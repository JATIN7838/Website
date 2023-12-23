<script>
  let cards = [
    {
      id: "c1",
      icon: "1",
      title:
        "Where<br><span class='glow'>Passion</span><br>Meets<br>Performance",
      image: "../images/01hero.jpg",
    },
    {
      id: "c2",
      icon: "2",
      title:
        "Bring<br>The<span class='glow'> Stage</span><br>To Your<br>Screen",
      image: "../images/02hero.jpg",
    },
    {
      id: "c3",
      icon: "3",
      title:
        "Connecting<br><span class='glow'>Hearts</span><br>Through Live<br>Artistry",
      image: "../images/03hero.jpg",
    },
  ];
  let selectedCard = cards[0].id; // Initialize with the id of the first card

  const changeCard = () => {
    const currentIndex = cards.findIndex((card) => card.id === selectedCard);
    const nextIndex = (currentIndex + 1) % cards.length;
    selectedCard = cards[nextIndex].id;
  };

  setInterval(changeCard, 5000);
</script>

<div class="container">
  {#each cards as card (card.id)}
    <input
      type="radio"
      name="slide"
      id={card.id}
      bind:group={selectedCard}
      value={card.id}
    />
    <label
      for={card.id}
      class="card"
      style="background-image: url({card.image});"
      ><div class="logo">
        <p></p>
      </div>
      <div class="title">{@html card.title}</div>
      <div class="icon">{card.icon}</div>
    </label>
  {/each}
</div>

<style>
  :global(.glow) {
    outline: none;
    animation: animate 5s linear infinite;
  }

  @keyframes animate {
    0%,
    18%,
    20%,
    50.1%,
    60%,
    65.1%,
    80%,
    90.1%,
    92% {
      color: hsl(183, 70%, 62%);
      text-shadow: 0 0 0.5em hsl(183, 70%, 62%);
    }
    18.1%,
    20.1%,
    30%,
    50%,
    60.1%,
    65%,
    80.1%,
    90%,
    92.1%,
    100% {
      color: #fff;
      text-shadow:
        0 0 10px hsl(183, 70%, 62%),
        0 0 20px hsl(183, 70%, 62%),
        0 0 40px hsl(183, 70%, 62%),
        0 0 50px hsl(183, 70%, 62%);
    }
  }
  .container {
    height: 500px;
    display: flex;
    flex-wrap: nowrap;
    justify-content: start;
  }

  .card {
    width: 80px;
    border-radius: 0.75rem;
    background-size: cover;
    /* background-position: center center; */
    overflow: hidden;
    border-radius: 2rem;
    margin: 0 10px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    transition: 0.6s cubic-bezier(0.28, -0.03, 0, 0.99);
    box-shadow: 0px 10px 30px -5px black;
  }

  .title {
    padding-left: 40px;
    padding-top: 40px;
    color: rgba(255, 255, 255, 0.9);
    font-size: 55px;
    font-weight: bold;
    /* give text shadow */
    text-shadow: 0px 0px 10px rgba(0, 0, 0, 1);
  }

  input:not(:checked) + label > .title {
    display: none;
  }

  .card > .icon {
    background: #333;
    color: white;
    border-radius: 50%;
    width: 50px;
    height: 50px;
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 18px;
  }

  input {
    display: none;
  }

  input:checked + label {
    width: 75vw;
    background-position: center center;
    transition: width 0.6s cubic-bezier(0.28, -0.03, 0, 0.99);
  }
  input:checked + label > .icon {
    background: white;
    color: #333;
    font-weight: bold;
  }
  @media (max-height: 600px) {
    .title {
      font-size: 45px;
      padding-top: 0;
    }
  }
  @media (max-height: 400px) {
    .card > .icon {
      opacity: 0;
    }
  }
  @media (max-height: 300px) {
    .card > .icon {
      opacity: 0;
    }
    .title {
      font-size: 30px;
    }
  }
  @media (max-width: 1000px) {
    .icon {
      width: 30px;
      height: 30px;
    }
    input:checked + label {
      width: 60vw;
    }

    .title {
      font-size: 50px;
    }
  }

  @media (max-width: 750px) {
    @keyframes flyIn {
      from {
        transform: translateX(-100%);
        opacity: 0;
      }
      to {
        transform: translateX(0);
        opacity: 1;
      }
    }
    .container {
      height: 300px;
    }
    input:checked + label {
      animation: flyIn 1s ease-out;
      width: 80vw;
    }

    input:not(:checked) + .card {
      display: none;
    }

    .title {
      font-size: 30px;
      padding-left: 20px;
    }
  }

  @media (max-width: 400px) {
    .title {
      font-size: 25px;
      padding-left: 15px;
    }
  }
  @media (max-width: 250px) {
    .title {
      font-size: 20px;
      padding-left: 10px;
    }
  }
</style>
