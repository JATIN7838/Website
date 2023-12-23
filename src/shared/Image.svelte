<div class="container">
  <img src="./images/homebmg.jpg" alt="View" />
</div>

<style>
  .container {
    margin: 0 20px;
    border-radius: 30px;
    box-shadow: 0px 0px 10px rgba(255, 255, 255, 0.7);
    height: 300px;
    width: 60vw;
    transform-style: preserve-3d;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .container img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 30px;
    transform: translateZ(50px);
  }
  @media (max-width: 1000px) {
    .container {
      width: 600px;
    }
  }
</style>
