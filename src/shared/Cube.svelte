<div class="cube">
  <div class="top"></div>
  <span style="--i:0;">
    <h2 class="content">17 Million</h2>
    <h2 class="content">17 Million</h2>
    <p class="content-p">Artists Worldwide</p>
    <p class="content-p">Artists Worldwide</p>
  </span>
  <span style="--i:1;">
    <h2 class="content">50%</h2>
    <h2 class="content">50%</h2>
    <p class="content-p">Regional Content Share</p>
    <p class="content-p">Regional Content Share</p>
  </span>
  <span style="--i:2;">
    <h2 class="content">17 Million</h2>
    <h2 class="content">17 Million</h2>
    <p class="content-p">Artists Worldwide</p>
    <p class="content-p">Artists Worldwide</p></span
  >
  <span style="--i:3;">
    <h2 class="content">50%</h2>
    <h2 class="content">50%</h2>
    <p class="content-p">Regional Content Share</p>
    <p class="content-p">Regional Content Share</p>
  </span>
</div>

<style>
  :root {
    --size: 200px;
    --title-size: 35px;
    --color: linear-gradient(-45deg, red, blue);
    --shadow-color: linear-gradient(45deg, blue, red);
    --text-size: 30px;
  }

  .content-p {
    position: absolute;
    left: -20px;
    text-align: center;
    font-size: var(--text-size);
    color: #fff;
    text-shadow:
      0 0 0.2em currentColor,
      0 0 0.3em currentColor;
    transform: translateZ(20px) translateY(10px) translateX(10px);
  }
  .content-p:nth-of-type(2) {
    transform: translateZ(0) translateY(20px) translateX(10px);
    color: rgba(0, 0, 0, 0.6);
    filter: blur(2px);
  }

  .content {
    position: absolute;
    top: 0px;
    font-weight: bold;
    font-size: var(--title-size);
    color: rgb(239, 88, 68);
    transform: translateZ(20px);
    text-shadow:
      0 0 0.2em currentColor,
      0 0 0.3em currentColor;
  }
  .content:nth-child(1) {
    transform: translateZ(0) translateY(10px);
    color: rgba(0, 0, 0, 0.5);
    filter: blur(2px);
  }

  .cube {
    margin-right: 60px;
    margin-left: 60px;
    position: relative;
    width: var(--size);
    height: var(--size);
    transform-style: preserve-3d;
    transform: rotateX(-30deg);
    animation: animate 10s linear infinite;
  }
  @keyframes animate {
    0% {
      transform: rotateX(-30deg) rotateY(0deg);
    }
    100% {
      transform: rotateX(-30deg) rotateY(360deg);
    }
  }
  .cube div {
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    transform-style: preserve-3d;
  }
  .cube span {
    position: absolute;
    width: 100%;
    height: 100%;
    background: var(--color);
    transform: rotateY(calc(var(--i) * 90deg)) translateZ(calc(var(--size) / 2));
    display: flex;
    justify-content: center;
    align-items: center;
    transform-style: preserve-3d;
  }

  .top {
    position: absolute;
    top: 0;
    left: 0;
    width: var(--size);
    height: var(--size);
    background: #222;
    transform: rotateX(90deg) translateZ(calc(var(--size) / 2));
  }
  .top::before {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    width: var(--size);
    height: var(--size);
    background: var(--shadow-color);
    transform: translateZ(calc(var(--size) * -1.2));
    filter: blur(20px);
    box-shadow:
      0 0 120px rgba(255, 0, 0, 0.2),
      0 0 200px rgba(255, 0, 0, 0.4),
      0 0 300px rgba(255, 0, 0, 0.6);
  }
  @media (max-width: 1000px) {
    :root {
      --size: 150px;
      --title-size: 25px;
      --text-size: 20px;
    }
  }
  @media (max-width: 300px) {
    :root {
      --size: 125px;
      --title-size: 20px;
      --text-size: 15px;
    }
  }
</style>
