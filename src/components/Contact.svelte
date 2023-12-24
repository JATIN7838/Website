<script>
  //import store
  import { isOpen } from "../store.js";

  let name = "";
  let email = "";
  let phone = "";

  const handleSubmit = (event) => {
    event.preventDefault();

    if (!name || !email || !phone) {
      alert("All fields are required");
      return;
    }
    let form = document.getElementById("contact-form");
    fetch(form.action, {
      method: "POST",
      body: new FormData(document.getElementById("contact-form")),
    }).then(function (response) {
      return response.json();
    });
    alert("Form Submitted Successfully");
    name = "";
    email = "";
    phone = "";
  };
</script>

<svelte:head>
  <script src="/scripts/particles.js"></script>
  <script src="/scripts/app.js"></script>
</svelte:head>
<div class="content" class:tilt={$isOpen}>
  <h1>Contact</h1>
  <h3
    style="color:#ef5744; font-size:20px; cursor:pointer; margin-top:15px;margin-bottom:10px;"
    on:click
    on:keypress
  >
    Home
  </h3>
  <div class="form-container">
    <div id="particles-js"></div>
    <div class="form">
      <form
        action="https://sheetdb.io/api/v1/co4j8b5gsmlq1"
        method="post"
        id="contact-form"
      >
        <h2>Fill Your Details</h2>
        <input
          bind:value={name}
          type="text"
          id="name"
          name="data[Name]"
          placeholder="Name"
          required
        /><br />
        <input
          bind:value={email}
          type="text"
          id="email"
          name="data[Email]"
          required
          placeholder="Email"
        /><br />
        <input
          bind:value={phone}
          type="text"
          id="phone"
          name="data[Phone]"
          placeholder="Phone"
          required
        /><br />
        <button type="Submit" on:click={handleSubmit}>Submit</button>
      </form>
    </div>
  </div>
  <div class="footer" class:tilt={$isOpen}>
    <h2>Copyright © 2023 Playyformee. All Rights Reserved.</h2>
  </div>
</div>

<style>
  #particles-js {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: 1;
  }
  button {
    width: 100px;
    color: white;
    background-color: #000000;
    margin-top: 10px;
    border-radius: 15px;
    font-weight: bold;
    cursor: pointer;
  }
  .form {
    width: 400px;
    position: absolute;
    height: 100%;
    z-index: 2;
    top: 20%;
  }
  input {
    width: 100%;
    background-color: white;
    border-radius: 10px;
    color: rgb(66, 66, 66);
    margin-top: 10px;
  }
  .form-container {
    width: 100%;
    height: 100%;
    position: relative;
    background: rgb(21, 21, 21);
    display: flex;
    justify-content: center;
    align-items: center;
  }
  h2 {
    color: #ffffff89;
    text-align: center;
  }
  .content {
    z-index: 1;
    width: 100%;
    height: 800px;
    background-color: rgb(22, 24, 36);
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
    transition: transform 0.5s ease;
    transform-origin: center left; /* Adjust as needed */
  }

  h1 {
    margin-top: 15px;
    margin-bottom: 0;
    font-size: 40px;
    color: white;
  }
  .footer {
    border-top: 1px solid #fff;
    z-index: 1;
    width: 100%;
    height: 150px;
    background: rgb(22, 24, 36);
    transition: transform 0.5s ease;
    transform-origin: center left;
  }

  .tilt {
    transform: perspective(1500px) rotateY(12deg) translateX(16vw); /* Default tilt for larger screens */
  }

  @media (max-width: 1000px) {
    .tilt {
      width: 80vw;
      transform: perspective(1200px) rotateY(10deg) translateX(20vw);
    }
  }
  @media (max-width: 500px) {
    h2 {
      font-size: 1em;
    }
  }
  @media (max-width: 450px) {
    .tilt {
      transform: perspective(1200px) rotateY(15deg) translateX(25vw);
    }

    .form {
      width: 80%;
    }
  }
</style>
