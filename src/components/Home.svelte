<script>
  //import store
  import { isOpen } from "../store.js";
  import Crousel from "../shared/Crousel.svelte";
  import Card from "../shared/Card.svelte";
  import Cube from "../shared/Cube.svelte";
  import Image from "../shared/Image.svelte";
  import Why from "./Why.svelte";
  import Support from "./Support.svelte";
  import Footer from "../shared/Footer.svelte";
  import { createEventDispatcher } from "svelte";
</script>

<div class="slider" class:tilt={$isOpen}>
  <Crousel />
</div>
<div class="about" class:tilt={$isOpen}>
  <span style="color:white; font-size:2.5em; text-shadow:0 0 20px black"
    >About Us</span
  >
  <span class="about-text"
    >At Playyformee, We're Dedicated To Redefining Live Entertainment. Our
    Platform Connects Artists And Audiences Worldwide In A New Era Of
    Interactive Performances. Join Us And Be Part Of The Magic!</span
  >

  <div class="pic-cube"><Image /><Cube /></div>
  <div class="card-container">
    <Card cardNo={0}></Card>
    <Card cardNo={1}></Card>
    <Card cardNo={2}></Card>
    <Card cardNo={3}></Card>
    <Card cardNo={4}></Card>
    <Card cardNo={5}></Card>
  </div>
</div>
<div class="why" class:tilt={$isOpen}><Why /></div>
<div class="support" class:tilt={$isOpen}><Support /></div>

<div class="footer" class:tilt={$isOpen}>
  <Footer on:click />
</div>

<style>
  :root {
    --about-height: 1200px;
    --footer-height: 400px;
  }
  .footer {
    border-top: 1px solid #fff;
    z-index: 1;
    width: 100%;
    height: var(--footer-height);
    background: rgb(22, 24, 36);
    transition: transform 0.5s ease;
    transform-origin: center left;
  }

  .support {
    box-sizing: border-box;
    display: flex;
    align-items: center;
    justify-content: space-evenly;
    flex-direction: column;
    width: 100%;
    height: 600px;
    background: rgb(22, 24, 36);
    transition: transform 0.5s ease;
    transform-origin: center left;
  }

  .why {
    box-sizing: border-box;
    display: flex;
    align-items: center;
    justify-content: space-evenly;
    flex-direction: column;
    width: 100%;
    height: 700px;
    background: rgb(22, 24, 36);
    transition: transform 0.5s ease;
    transform-origin: center left;
  }

  .about-text {
    display: block;
    text-align: center;
    padding: 0 30%;
    font-size: 18px;
    line-height: 30px;
    text-transform: capitalize;
    color: hsl(334, 7%, 95%);
    text-shadow: 0 0 0.5em currentColor;
    letter-spacing: 1px;
  }
  .pic-cube {
    width: 100%;
    height: 300px;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    align-items: center;
  }
  .about {
    z-index: 1;
    flex-wrap: wrap;
    width: 100%;
    height: var(--about-height);
    background: rgb(22, 24, 36);
    transition: transform 0.5s ease;
    transform-origin: center left;
    display: flex;
    align-items: center;
    justify-content: space-evenly;
  }

  .card-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-evenly;
    width: 100%;
  }

  .slider {
    z-index: 1;
    width: 100%;
    height: 550px;
    background: linear-gradient(-45deg, #d2001a, #7462ff, #f48e21, #23d5ab);
    animation: color 12s ease-in-out infinite;
    background-size: 300% 300%;
    display: flex;
    justify-content: center;
    align-items: center;
    transition: transform 0.5s ease;
    transform-origin: center left; /* Adjust as needed */
  }

  @keyframes color {
    0% {
      background-position: 0% 50%;
    }
    50% {
      background-position: 100% 50%;
    }
    100% {
      background-position: 0% 50%;
    }
  }

  .tilt {
    transform: perspective(1500px) rotateY(12deg) translateX(16vw); /* Default tilt for larger screens */
  }
  @media (max-width: 1500px) {
    :root {
      --about-height: 1500px;
    }
  }

  @media (max-width: 1000px) {
    .support {
      height: 1200px;
    }
  }
  @media (max-width: 910px) {
    .about-text {
      padding: 0 20%;
    }
    :root {
      --about-height: 1800px;
    }
    .pic-cube {
      height: 600px;
    }
    .tilt {
      width: 80vw;
      transform: perspective(1200px) rotateY(10deg) translateX(20vw);
    }
    :root {
      --why-height: 800px;
    }
    .why {
      height: 800px;
      justify-content: space-between;
    }
  }
  @media (max-width: 750px) {
    .slider {
      height: 400px;
    }
  }
  @media (max-width: 600px) {
    :root {
      --about-height: 2700px;
    }
  }
  @media (max-width: 450px) {
    .about-text {
      padding: 0 10%;
    }
    .tilt {
      transform: perspective(1200px) rotateY(15deg) translateX(25vw);
    }
    .why {
      height: 1250px;
    }
    .support {
      height: 1800px;
    }
  }

  @media (max-width: 300px) {
    .about-text {
      padding: 0 5%;
      font-size: 16px;
    }
    :root {
      --about-height: 3000px;
    }
  }
</style>
