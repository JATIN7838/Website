<script>
  import { onMount } from "svelte";
  import VanillaTilt from "vanilla-tilt";
  let pre;
  let text;
  onMount(() => {
    VanillaTilt.init(pre, {
      max: 35,
      speed: 400,
    });
    pre.addEventListener("tiltChange", (event) => {
      const { tiltX, tiltY } = event.detail;

      text.style.transform = `translateX(${tiltX}px) translateY(${-tiltY}px)`;
    });
  });
  export let cardNo;
  let cards = [
    {
      id: 0,
      title: "Elevating Artistry",
      description:
        "We're On A Mission To Empower Artists From Around The World To Showcase Their Talents And Creativity.",
    },
    {
      id: 1,
      title: "Seamless Connections",
      description:
        "Our Platform Connects Remote Artists With A Global Audience, Breaking Down Geographical Barriers.",
    },
    {
      id: 2,
      title: "Endless Possibilities",
      description:
        "Singers, Dancers, Comedians, And More. We Welcome All Forms Of Artistic Expression And Experience The Future Of Entertainment.",
    },
    {
      id: 3,
      title: "Virtual Stages",
      description:
        "Discover A World Of Talent, From Live Shows To Captivating Reels, All From The Comfort Of Your Mobile Device.",
    },
    {
      id: 4,
      title: "Easy Bookings",
      description:
        "With Just A Few Taps, You Can Reserve Your Front-Row Seat To The Next Big Performance And Be Part Of A Creative Revolution.",
    },
    {
      id: 5,
      title: "Event Wizards",
      description:
        "We Take The Hassle Out Of Organizing, Making Sure Artists Can Focus On Their Art While We Handle The Logistics.",
    },
  ];
</script>

<div class="pre" bind:this={pre}>
  <div class="content">
    <div class="text" bind:this={text}>
      <span class="token selector">0{cardNo + 1}</span><br />
      <span class="token property glow">{cards[cardNo].title}</span><br /><br />
      <span class="token punctuation">{cards[cardNo].description}</span>
    </div>
  </div>
</div>

<style>
  .text {
    transform: translateZ(25px);
    transition: transform 0.3s ease-out;
    transform-style: preserve-3d;
  }
  .content {
    box-sizing: border-box;
    background: hsl(222, 45%, 7%);
    border-radius: 1rem;
    width: 100%;
    height: 100%;
    padding-left: 20px;
    padding-right: 10px;
    box-shadow:
      0px 0px 10px rgba(0, 0, 0, 1),
      0px 0px 15px rgba(0, 0, 0, 1);
    transform: translateZ(40px);
    transform-style: preserve-3d;
    overflow: none;
    /* blur the borer radius */
  }

  :root {
    --pink: hsl(338, 70%, 55%);
    --teal: hsl(183, 70%, 62%);
    --white: hsl(334, 7%, 95%);
  }

  .pre {
    margin: 0 20px;
    height: 225px;
    width: 25vw;
    --selector: var(--pink);
    --property: var(--teal);
    --punctuation: var(--white);
    --undefined: var(--white);
    background: linear-gradient(-45deg, red, blue);
    color: var(--undefined);
    padding: 1.5rem;
    border-radius: 1rem;
    box-shadow: 0px 0px 10px rgba(255, 255, 255, 0.7);
    margin-top: 30px;
    transform-style: preserve-3d;

    /* perspective: 2000px; */
  }

  .pre > * {
    text-shadow: 0 0 0.5em currentColor;
  }

  .selector {
    transform: translateZ(35px);
    font-size: 45px;
    font-weight: bold;
    color: var(--selector);
  }

  .property {
    transform: translateZ(35px);
    font-size: 25px;
    font-weight: bold;
    color: var(--property);
  }

  .punctuation {
    transform: translateZ(25px);
    font-size: 18px;
    color: var(--punctuation);
  }

  @media (max-width: 1225px) {
    .pre {
      width: 35vw;
    }
  }

  @media (max-width: 900px) {
    /* .pre {
      width: 40vw;
    } */
    .property {
      font-size: 18px;
    }
    .selector {
      font-size: 35px;
    }
    .punctuation {
      font-size: 15px;
    }
  }

  @media (max-width: 600px) {
    .pre {
      width: 300px;
    }
    .property {
      font-size: 20px;
    }
    .selector {
      font-size: 45px;
    }
    .punctuation {
      font-size: 15px;
    }
  }
  @media (max-width: 400px) {
    .pre {
      width: 250px;
    }
    .property {
      font-size: 20px;
    }
    .selector {
      font-size: 35px;
    }
    .punctuation {
      font-size: 15px;
    }
  }
  @media (max-width: 350px) {
    .pre {
      width: 230px;
    }
  }
  @media (max-width: 300px) {
    .pre {
      width: 180px;
      height: 260px;
    }
    .property {
      font-size: 18px;
    }
    .selector {
      font-size: 35px;
    }
    .punctuation {
      font-size: 13px;
    }
    .content {
      overflow: hidden;
    }
  }
</style>
