<script>
  import Streampage from "./Streampage.svelte";
  import { inShow } from "../store.js";
  const appId = "f4ba96e713644580be925491db5127a0";
  let channel;
  let token; // Fetch this from your token server

  // Fetch the token from your server
  async function fetchToken() {
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
    //check token type
    token = resp.token;
    inShow.update((n) => true);
    channel = "";
  }
</script>

<div class="container">
  {#if $inShow}
    <Streampage {appId} {channel} {token} />
  {:else}
    <h3>Please input the channel name</h3>
    <br />
    <input bind:value={channel} /><br />
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
</style>
