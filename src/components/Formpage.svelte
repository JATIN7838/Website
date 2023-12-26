<script>
  import Streampage from "./Streampage.svelte";
  const appId = "f4ba96e713644580be925491db5127a0";
  const channel = "test";
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
  }
</script>

<div class="container">
  {#if token}
    <Streampage {appId} {channel} {token} />
  {:else}
    <button on:click={fetchToken}> Join</button>
  {/if}
</div>

<style>
  .container {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100vh;
    background-color: rgb(22, 24, 36);
  }
</style>
