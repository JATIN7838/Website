<script>
  let cards = [
    {
      title: "Multi Device Support",
      text: "Anytime, Anywhere, Smooth And Seamless Cross Platform Services On All Types Of Device",
      icon: "fa-solid fa-desktop",
    },
    {
      title: "All-In-One Artist Heaven",
      text: "Holistic Platform, From Organizing To Managing Shows",
      icon: "fa-solid fa-users-viewfinder",
    },
    {
      title: "Multilingual Support And Comfort",
      text: "Global Language, Unparalleled Audio And Visual Excellence",
      icon: "fa-solid fa-language",
    },
    {
      title: "Crisp & Clear Streaming",
      text: "Elevate Your Senses With 4K Video And Crystal-Clear Audio",
      icon: "fa-solid fa-video",
    },
  ];
</script>

<svelte:head>
  <script
    src="https://kit.fontawesome.com/0df4c92ac2.js"
    crossorigin="anonymous"
  ></script>
</svelte:head>

<span class="title">Our Supports</span>
<div class="container">
  {#each cards as card (card)}
    <div class="card">
      <div class="icon">
        <i class={card.icon}></i>
      </div>
      <div class="content">
        <span>{card.title}</span>
        <p>{card.text}</p>
      </div>
    </div>
  {/each}
</div>

<style>
  :root {
    --top-radius: 30px;
  }
  .content {
    position: relative;
    width: 100%;
    text-align: center;
    padding: 30px 20px;
  }
  .content span {
    color: black;
    /* text-shadow: 0 0 20px black; */
    font-weight: bold;
    font-size: 25px;
  }
  .content p {
    font-weight: bold;
    font-size: 15px;
    color: white;
    text-shadow: 0 0 20px black;
  }

  .icon i {
    color: white;
    font-size: 3em;
    position: relative;
    z-index: 2;
  }
  .title {
    color: white;
    font-size: 2.5em;
    text-shadow: 0 0 20px black;
  }
  .container {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    background-color: rgb(22, 24, 36);
    width: 95%;
    height: 500px;
  }
  .card {
    position: relative;
    width: 20vw;
    height: 400px;
    margin: 20px;
    border-bottom-left-radius: 160px;
    border-bottom-right-radius: 160px;
    border-top-left-radius: var(--top-radius);
    border-top-right-radius: var(--top-radius);
    box-shadow:
      0 15px 0 #fff,
      inset 0 -15px 0 rgba(255, 255, 255, 0.25),
      0 35px 0 rgba(168, 168, 168, 0.2);
    overflow: hidden;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-content: flex-start;
  }
  .card::before {
    content: "";
    position: absolute;
    top: -140px;
    left: -40%;
    width: 100%;
    height: 120%;
    background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2));
    transform: rotate(35deg);
    filter: blur(1px);
    pointer-events: none;
  }
  .card:nth-child(1) {
    background: linear-gradient(to bottom, #ff2ae0, #645bf6);
  }
  .card:nth-child(2) {
    background: linear-gradient(to bottom, #ffec61, #f321d7);
  }
  .card:nth-child(3) {
    background: linear-gradient(to bottom, #24ff72, #9a4eff);
  }
  .card:nth-child(4) {
    background: linear-gradient(to bottom, #ff2a2a, #ff9a2a);
  }
  .icon {
    position: relative;
    width: 140px;
    height: 120px;
    background: rgb(22, 24, 36);
    border-bottom-left-radius: 100px;
    border-bottom-right-radius: 100px;
    z-index: 2;
    box-shadow:
      0 10px 0 rgba(0, 0, 0, 0.4),
      inset 0 -8px 0 rgb(255, 255, 255);
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .icon::before {
    content: "";
    position: absolute;
    top: 0;
    left: -50px;
    width: 50px;
    height: 50px;
    background: transparent;
    border-top-right-radius: var(--top-radius);
    box-shadow: 15px -15px 0 15px rgb(22, 24, 36);
  }
  .icon::after {
    content: "";
    position: absolute;
    top: 0;
    right: -50px;
    width: 50px;
    height: 50px;
    background: transparent;
    border-top-left-radius: var(--top-radius);
    box-shadow: -15px -15px 0 15px rgb(22, 24, 36);
  }
  @media (max-width: 1200px) {
    :root {
      --top-radius: 15px;
    }
    .card {
      width: 18vw;
    }
    .content span {
      font-size: 22px;
    }
  }
  @media (max-width: 995.5px) {
    .card {
      width: 30vw;
    }
    .container {
      height: 1000px;
      justify-content: space-around;
    }
  }
  @media (max-width: 650px) {
    .card {
      width: 40vw;
      margin: 10px;
    }
    .content span {
      font-size: 20px;
    }
  }
  @media (max-width: 450px) {
    .card {
      width: 60vw;
      height: 300px;
    }
    .content span {
      font-size: 15px;
    }
    .content p {
      font-size: 12px;
    }

    .container {
      height: 1600px;
    }
  }
  @media (max-width: 300px) {
    .icon {
      width: 100px;
      height: 105px;
      box-shadow:
        0 5px 0 rgba(0, 0, 0, 0.4),
        inset 0 -4px 0 rgb(255, 255, 255);
    }
  }
</style>
