<div class="contact">
  <span> More Info Coming Soon - Connect With Us To Stay Updated.</span>
  <button on:click>CONTACT US</button>
</div>
<div class="copywrite">
  <h2>Copyright © 2023 Playyformee. All Rights Reserved.</h2>
</div>

<style>
  .contact {
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 100%;
    height: 70%;
  }
  .copywrite {
    border-top: 1px solid #ffffff3f;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    height: auto;
  }
  h2 {
    color: #ffffff89;
    text-align: center;
  }
  span {
    width: 50%;
    padding-left: 50px;
    color: white;
    font-weight: bold;
    font-size: 1.5em;
    text-align: center;
  }
  button {
    font-weight: bold;
    color: white;
    width: 150px;
    font-size: 1em;
    margin-right: 30px;
    background-color: #ef5744;
    cursor: pointer;
    border-radius: 20px;
  }

  @media (max-width: 500px) {
    .contact {
      flex-direction: column;
      justify-content: center;
      align-items: center;
    }
    span {
      width: 90%;
      padding: 0;
    }
    button {
      margin: 15px 0;
    }
    h2 {
      font-size: 1em;
    }
  }
</style>
