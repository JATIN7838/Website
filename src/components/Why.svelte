<script>
  let cards = [
    {
      title: "Reel Magic",
      text: "Experience Art In Bitesize Brilliance",
      icon: "fa-solid fa-film",
    },
    {
      title: "Follow & Discover",
      text: "Stay In Sync With Your Favorite Artists",
      icon: "fa-solid fa-user-plus",
    },
    {
      title: "Book Your Spot",
      text: "Front-Row Reservations At Your Fingertips",
      icon: "fa-solid fa-ticket",
    },
    {
      title: "Host With Ease",
      text: "Your Stage, Your Rules - Show Hosting Made Simple",
      icon: "fa-solid fa-microphone-lines",
    },
  ];
</script>

<svelte:head>
  <script
    src="https://kit.fontawesome.com/0df4c92ac2.js"
    crossorigin="anonymous"
  ></script>
</svelte:head>

<span class="title">Why PlayyForMee</span>
<div class="container">
  <div class="card-container">
    {#each cards as card (card)}
      <div class="card">
        <i class={card.icon}></i>
        <span class="glow">{card.title}</span>
        <p>{card.text}</p>
      </div>
    {/each}
  </div>
  <div class="video">
    <video autoplay loop muted>
      <source src="./images/homepage_vid.mp4" type="video/mp4" />
      Your browser does not support the video tag.
    </video>
  </div>
</div>

<style>
  :root {
    --pink: hsl(338, 70%, 55%);
    --teal: hsl(183, 70%, 62%);
    --white: hsl(334, 7%, 95%);
  }
  p {
    z-index: 2;
    text-align: center;
    color: var(--white);
  }
  i {
    z-index: 2;
    font-size: 70px;
    color: var(--pink);
  }
  .card span {
    z-index: 2;
    margin-top: 5px;
    font-size: 1.25em;
    font-weight: bold;
    color: var(--teal);
  }
  .card {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 10px;
    height: auto;
    width: auto;
    background-color: rgb(22, 24, 36);
    border-radius: 30px;
    box-shadow: 0px 0px 10px rgba(255, 255, 255, 0.7);
    overflow: hidden;
    position: relative;
  }

  .card::before {
    content: "";
    position: absolute;
    width: 120px;
    height: 500px;
    background: linear-gradient(-45deg, red, blue, red);
    box-shadow: 0 0 20px rgb(8, 8, 8);
    animation: animate 2s linear infinite;
  }
  .card::after {
    content: "";
    position: absolute;
    inset: 5px;
    background-color: rgb(4, 75, 97);
    border-radius: 30px;
  }
  @keyframes animate {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }

  .card > * {
    text-shadow: 0 0 0.5em currentColor;
  }
  .card-container {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-template-rows: repeat(2, 1fr);
    gap: 40px;
    align-items: stretch;
    height: auto;
    width: 48vw;
  }
  .container {
    height: 70%;
    width: 100%;
    display: flex;
    justify-content: space-evenly;
    align-items: center;
  }
  video {
    height: 100%;
    width: 100%;
    object-fit: cover;
    border-radius: 30px;
  }
  .video {
    width: 37vw;
    height: 100%;
    background-color: #fff;
    border-radius: 30px;
    box-shadow: 0px 0px 10px rgba(255, 255, 255, 0.7);
  }
  .title {
    font-size: 2.5em;
    color: #fff;
    text-align: center;
    width: 100%;
    text-shadow: 0 0 0.5em black;
    margin-top: 40px;
  }

  @media (max-width: 995px) {
    .container {
      height: 55%;
    }

    i {
      font-size: 40px;
    }
    p {
      font-size: 14px;
    }

    .card span {
      font-size: 1em;
    }
  }

  @media (max-width: 900px) {
    .container {
      flex-direction: column-reverse;
      justify-content: space-between; /* Add this */
    }
    .video {
      width: 80vw;
      height: 300px;
      margin-bottom: 40px;
    }
    .card-container {
      width: 80vw;
    }
  }
  @media (max-width: 450px) {
    .container {
      height: 100%;
    }
    .title {
      font-size: 30px;
    }
    .card-container {
      display: flex;
      flex-wrap: wrap;
    }
    .card {
      width: 80vw;
      height: 150px;
    }
    .video {
      height: 250px;
      margin-top: 40px;
    }
  }
</style>
