<script>
  import Streampage from "./Streampage.svelte";
  import { inShow } from "../store.js";
  const appId = "f4ba96e713644580be925491db5127a0";
  let channel = "";
  let token;
  let isLoading = false;
  let text = "Please input channel name";

  async function fetchToken() {
    if (channel == "") {
      text = "Invalid channel";
      return;
    }
    isLoading = true;
    const response = await fetch(
      "https://playforme-be4a66830edf.herokuapp.com/getToken",
      {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          tokenType: "rtc",
          uid: "0",
          channel: channel,
          role: "publisher",
          expire: 3600,
        }),
      }
    );
    let resp = await response.json();
    isLoading = false;
    token = resp.token;
    inShow.update(() => true);
  }
</script>

<div class="container">
  {#if isLoading}
    <h1
      style="
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        color: #fff;
      "
    >
      Loading...
    </h1>
  {:else if $inShow}
    <Streampage {appId} {channel} {token} />
  {:else}
    <h3>{text}</h3>
    <input bind:value={channel} />
    <button on:click={fetchToken}>Join</button>
  {/if}
</div>

<style>
  .container {
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
    width: 100%;
    height: 100vh;
    background-color: rgb(22, 24, 36);
  }
  .container h3 {
    color: white;
  }
</style>
