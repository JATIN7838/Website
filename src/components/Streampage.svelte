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
    }
    track = await AgoraRTC.createCameraVideoTrack();
    track.play("camera-video");
    if (isJoined) {
      await client.publish(track);
      isVideoPubed = true;
    }
  }

  async function turnOnMicrophone() {
    isAudioOn = !isAudioOn;

    if (audioTrack) {
      return audioTrack.setEnabled(!audioTrack.enabled);
    }

    audioTrack = await AgoraRTC.createMicrophoneAudioTrack();
    audioTrack.play();

    if (isJoined) {
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
    isJoined = false;
    isAudioPubed = false;
    isVideoPubed = false;
    track && track.stop();
    audioTrack && audioTrack.stop();
    client && (await client.leave());
    //update inshow
    inShow.update((n) => false);
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

  // async function publishVideo() {
  //   if (!isVideoOn) {
  //     await turnOnCamera();
  //   }

  //   if (!isJoined) {
  //     await joinChannel();
  //   }
  //   await client.publish(track);
  //   isVideoPubed = true;
  // }

  // async function publishAudio() {
  //   if (!isAudioOn) {
  //     await turnOnMicrophone();
  //   }
  //   if (!isJoined) {
  //     await joinChannel();
  //   }

  //   isAudioPubed = true;
  // }
</script>

<div class="left-side">
  <h3>Pleat check you camera / microphone!</h3>
  <div class="buttons">
    <button on:click={turnOnCamera} class={isVideoOn ? "button-on" : ""}>
      Turn {isVideoOn ? "off" : "on"} camera
    </button>
    <button on:click={turnOnMicrophone} class={isAudioOn ? "button-on" : ""}>
      Turn {isAudioOn ? "off" : "on"} Microphone
    </button>
  </div>

  <div class="buttons">
    <!-- <button on:click={publishVideo} class={isVideoPubed ? "button-on" : ""}>
      Publish Video
    </button>
    <button on:click={publishAudio} class={isAudioPubed ? "button-on" : ""}>
      Publish Audio
    </button> -->
    <button on:click={leaveChannel}>Leave Channel</button>
  </div>
</div>
<div class="right-side">
  <video id="camera-video">
    <track kind="captions" />
  </video>
  <video id="remote-video">
    <track kind="captions" />
  </video>

  {#if isJoined && !isVideoSubed}
    <div class="waiting">
      In Show: {channel}
    </div>
  {/if}
</div>

<style>
</style>
