<script>
  import AgoraRTC from "agora-rtc-sdk-ng";
  import { inShow } from "../store.js";
  let track;
  let audioTrack;
  let client;

  let isJoined = false;
  let isAudioPubed = false;
  let isVideoPubed = false;
  let isAudioSubed = false;
  let isVideoSubed = false;

  let isVideoOn = false;
  let isAudioOn = false;

  async function turnOnCamera() {
    isVideoOn = !isVideoOn;

    if (track) {
      return track.setEnabled(!track.enabled);
    } else {
      track = await AgoraRTC.createCameraVideoTrack();
      track.play("camera-video");
    }
    if (isJoined && !isVideoPubed) {
      await client.publish(track);
      isVideoPubed = true;
    }
  }

  async function turnOnMicrophone() {
    isAudioOn = !isAudioOn;

    if (audioTrack) {
      return audioTrack.setEnabled(!audioTrack.enabled);
    } else {
      audioTrack = await AgoraRTC.createMicrophoneAudioTrack();
      audioTrack.play();
    }

    if (isJoined && !isAudioPubed) {
      await client.publish(audioTrack);
      isAudioPubed = true;
    }
  }

  export let channel;
  export let appId;
  export let token;

  async function joinChannel() {
    if (!client) {
      client = AgoraRTC.createClient({
        mode: "rtc",
        codec: "vp8",
      });

      client.on("user-published", onUserPublish);
    }

    await client.join(appId, channel, token, null);

    isJoined = true;
  }

  async function leaveChannel() {
    if (audioTrack) {
      audioTrack.setEnabled(false);
      audioTrack.stop();
      audioTrack.close();
    }
    if (track) {
      track.setEnabled(false);
      track.stop();
      track.close();
    }
    if (client) {
      await client.leave();
    }

    isJoined = false;
    isAudioPubed = false;
    isVideoPubed = false;
    window.location.reload();
  }

  async function onUserPublish(user, mediaType) {
    if (mediaType === "video") {
      const remoteTrack = await client.subscribe(user, mediaType);
      remoteTrack.play("remote-video");
      isVideoSubed = true;
    }
    if (mediaType === "audio") {
      const remoteTrack = await client.subscribe(user, mediaType);
      remoteTrack.play();
      isAudioSubed = true;
    }
  }
  joinChannel();
</script>

<div class="video-area">
  <video id="camera-video">
    <track kind="captions" />
  </video>
  <video id="remote-video">
    <track kind="captions" />
  </video>
</div>
<div class="button-area">
  <button on:click={turnOnCamera} class={isVideoOn ? "button-on" : ""}>
    Turn {isVideoOn ? "off" : "on"} camera
  </button>
  <button on:click={turnOnMicrophone} class={isAudioOn ? "button-on" : ""}>
    Turn {isAudioOn ? "off" : "on"} Microphone
  </button>
  <button on:click={leaveChannel}>Leave Channel</button>
</div>

<style>
  .video-area {
    display: flex;
    justify-content: space-evenly;
    align-items: center;
    width: 100%;
    height: 500px;
    background-color: rgb(22, 24, 36);
  }
  .video-area video {
    width: 40%;
    height: 100%;
  }
  .button-area {
    margin-top: 20px;
    display: flex;
    justify-content: space-evenly;
    align-items: center;
    width: 60%;
    height: 100px;
    background-color: rgb(22, 24, 36);
  }
</style>
