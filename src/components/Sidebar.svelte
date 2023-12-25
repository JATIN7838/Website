<script>
  import { createEventDispatcher } from "svelte";
  //import the store
  import { isOpen } from "../store.js";
  let dispatch = createEventDispatcher();
  export let currentTab = "Home";
  function toggleSidebar() {
    isOpen.update((n) => !n);
  }
  function sendCurrentTab(tab) {
    if (currentTab != tab) {
      dispatch("ChangeTab", tab);
    }
  }
</script>

<svelte:head>
  <link
    rel="stylesheet"
    href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css"
    integrity="sha512-DTOQO9RWCH3ppGqcWaEA1BIZOC6xxalwEsw9c2QQeAIftl+Vegovlnee1c9QX4TctnWMn13TZye+giMm8e2LwA=="
    crossorigin="anonymous"
    referrerpolicy="no-referrer"
  />
</svelte:head>

<button class="sidebar-btn" on:click={toggleSidebar} class:open={$isOpen}>
  {#if !$isOpen}
    <i class="fa fa-bars" aria-hidden="true"></i>
  {:else}
    <i class="fa fa-arrow-left" aria-hidden="true"></i>
  {/if}
</button>
<aside class:open={$isOpen}>
  <nav>
    <div class="logo-container">
      <img class="logo" src="./images/logo.png" alt="Logo" />
    </div>
    <hr
      style="width: 100%; color: white; height: 1px; background-color:white;"
    />
    <ul class="link-list">
      <li>
        <p
          class:current={currentTab === "Home"}
          id="Home"
          on:click={() => sendCurrentTab("Home")}
          on:keypress
          class:navitem={currentTab != "Home"}
        >
          Home
        </p>
      </li>
      <li>
        <p
          class:current={currentTab === "Contact"}
          id="Contact"
          on:click={() => sendCurrentTab("Contact")}
          on:keypress
          class:navitem={currentTab != "Contact"}
        >
          Contact
        </p>
      </li>
      <li>
        <p
          class:current={currentTab === "Shows"}
          id="Shows"
          on:click={() => sendCurrentTab("Shows")}
          on:keypress
          class:navitem={currentTab != "Shows"}
        >
          Shows
        </p>
      </li>
    </ul>
  </nav>
</aside>
<div class="main-content"></div>

<style>
  p {
    color: white;
  }
  .current {
    cursor: default;
    font-weight: bold;
    color: #fff;
    text-shadow:
      0 0 10px #37d0ff,
      0 0 20px #37d0ff,
      0 0 40px #37d0ff,
      0 0 80px #37d0ff,
      0 0 160px #37d0ff;
  }
  .logo {
    width: 7vw;
    height: 6vw;
  }
  .sidebar-btn {
    z-index: 10;
    position: fixed;
    left: 1vw;
    top: 50%;
    transition: left 0.3s ease;
    width: 50px; /* specify a fixed width */
    height: 50px; /* specify a fixed height */
    border-radius: 50%; /* make it round */
  }

  .sidebar-btn.open {
    left: 20vw;
    transition: all 0.8s ease;
  }
  .sidebar-btn i {
    font-size: 20px;
    transition: all 0.6s ease;
  }

  .sidebar-btn:hover {
    cursor: pointer;
    transition: all 0.8s ease;
    background-color: #f34b4b;
  }
  .sidebar-btn:hover i {
    color: white;
  }

  aside {
    position: fixed;
    top: 0;
    left: 0;
    bottom: 0;
    width: 8vw;
    transform: translateX(-200%);
    transition: transform 0.3s ease;
    background-color: #333;
    padding: 1em;
    border-right: 1px solid white;
  }

  aside.open {
    transform: translateX(0);
  }

  .navitem {
    padding: 0;
    font-size: 18px;
    color: white;
  }

  .navitem:hover {
    color: #f34b4b;
    cursor: pointer;
    text-decoration: none;
    font-size: 20px;
    font-weight: bold;
  }

  .logo-container {
    flex: 1;
    display: flex;
    align-items: flex-start;
    justify-content: center;
  }

  .link-list {
    list-style: none;
    padding: 0;
    padding-top: 35px;
    flex: 1;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
  @media (min-width: 1000px) {
    .sidebar-btn.open {
      left: 12vw;
    }
  }
  @media (max-width: 999.99px) {
    .sidebar-btn.open {
      left: 14vw;
    }
    .logo {
      width: 11vw;
      height: 10vw;
    }
  }
  @media (max-width: 675px) {
    .navitem {
      font-size: 16px;
    }
    .navitem:hover {
      font-size: 16px;
    }
    .sidebar-btn.open {
      left: 16vw;
    }
    .sidebar-btn {
      width: 35px;
      height: 35px;
    }
  }

  @media (max-width: 450px) {
    .logo {
      width: 12vw;
      height: 11vw;
    }
    .sidebar-btn.open {
      left: 20vw;
    }
    .navitem {
      font-size: 14px;
    }
    .navitem:hover {
      font-size: 14px;
    }
  }
  @media (max-width: 350px) {
    .logo {
      width: 16vw;
      height: 16vw;
    }
    .sidebar-btn.open {
      left: 22vw;
    }
    .navitem {
      font-size: 12px;
    }
    .navitem:hover {
      font-size: 12px;
    }
  }
</style>
