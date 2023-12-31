<script>
  import AgoraRTC from "agora-rtc-sdk-ng";

  let track;
  let audioTrack;
  let client;

  let isJoined = false;
  let isAudioPubed = false;
  let isVideoPubed = false;
  let remoteUsers = [];
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
      client.on("user-unpublished", onUserUnpublish);

      client.on("user-left", (user) => {
        const videoContainer = document.getElementById(`${user.uid}-container`);
        if (videoContainer) {
          videoContainer.remove();
        }
        remoteUsers = remoteUsers.filter(
          (remoteUser) => remoteUser.uid !== user.uid
        );
      });
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
    const remoteTrack = await client.subscribe(user, mediaType);

    if (mediaType === "video") {
      let videoContainer = document.getElementById(`${user.uid}-container`);

      // If the videoContainer div doesn't exist, create a new one
      if (!videoContainer) {
        videoContainer = document.createElement("div");
        videoContainer.id = `${user.uid}-container`;
        videoContainer.style.width = "100%";
        videoContainer.style.height = "400px";
        videoContainer.style.display = "flex";
        videoContainer.style.justifyContent = "center";
        videoContainer.style.alignItems = "center";
        videoContainer.style.margin = "10px 0";
        document.getElementById("remote-videos").appendChild(videoContainer);
      }

      let videoElement = document.getElementById(`${user.uid}-video`);
      if (!videoElement) {
        videoElement = document.createElement("video");
        videoElement.id = `${user.uid}-video`;
        videoElement.style.borderRadius = "20px";
        videoElement.style.width = "98%";
        videoElement.style.height = "100%";
        videoContainer.appendChild(videoElement);
      }
      // setTimeout(() => {
      //   videoElement.style.objectFit = "contain";
      // }, 100);

      remoteTrack.play(videoElement);
      videoElement.poster = "noposter.jpg";

      remoteUsers = [
        ...remoteUsers,
        { uid: user.uid, track: remoteTrack, mediaType: mediaType },
      ];
    }
    if (mediaType === "audio") {
      remoteTrack.play();
    }
  }
  async function onUserUnpublish(user) {
    const videoElement = document.getElementById(`${user.uid}-video`);
    if (videoElement) {
      videoElement.pause(); // Pause the video
      videoElement.removeAttribute("src"); // Clear the source
      videoElement.load(); // Load the video element
      videoElement.poster = "noposter.jpg"; //
    }
  }

  joinChannel();
</script>

<div class="video-area">
  <div id="local-video">
    <video id="camera-video">
      <track kind="captions" />
    </video>
  </div>
  <div id="remote-videos"></div>
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
    height: 90vh;
    width: 100%;
    justify-content: space-evenly;
    margin: 10px 0;
  }

  #local-video {
    width: 45%;
    border: 2px solid #ccc;
    border-radius: 20px;
  }

  #camera-video {
    width: 100%;
    height: 100%;
    object-fit: contain;
    border-radius: 20px;
  }
  #remote-videos {
    width: 45%;
    height: 100%;
    overflow-y: auto;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    border: 2px solid #ccc;
    border-radius: 20px;
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
