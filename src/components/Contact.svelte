<script>
  //import store
  import { isOpen } from "../store.js";
</script>

<div class="content" class:tilt={$isOpen}>
  <h1>Contact</h1>
</div>

<style>
  .content {
    z-index: 1;
    width: 100vw;
    height: 100vh;
    background-color: aqua;
    display: flex;
    justify-content: center;
    align-items: center;
    transition: transform 0.5s ease;
    transform-origin: center left; /* Adjust as needed */
  }
  .content.tilt {
    transform: perspective(1500px) rotateY(12deg) translateX(16vw); /* Default tilt for larger screens */
  }

  @media (max-width: 1000px) {
    .content.tilt {
      width: 80vw;
      transform: perspective(1200px) rotateY(10deg) translateX(20vw);
    }
  }
  @media (max-width: 450px) {
    .content.tilt {
      transform: perspective(1200px) rotateY(15deg) translateX(25vw);
    }
  }
</style>
