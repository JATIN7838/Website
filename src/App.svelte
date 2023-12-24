<script>
  import Sidebar from "./components/Sidebar.svelte";
  import Home from "./components/Home.svelte";
  import Contact from "./components/Contact.svelte";
  let currentTab = "Contact";
  function changeTab(event) {
    currentTab = event.detail;
  }
</script>

<main>
  <Sidebar {currentTab} on:ChangeTab={changeTab} />
  {#if currentTab == "Home"}
    <Home
      on:click={() => {
        currentTab = "Contact";
      }}
    />
  {:else if currentTab == "Contact"}
    <Contact
      on:click={() => {
        currentTab = "Home";
      }}
    />
  {/if}
</main>

<style>
</style>
