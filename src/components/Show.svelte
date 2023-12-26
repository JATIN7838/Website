<script>
  import { initializeApp } from "firebase/app";
  import {
    getAuth,
    GoogleAuthProvider,
    signInWithEmailAndPassword,
    signInWithRedirect,
    signOut,
  } from "firebase/auth";
  import Formpage from "./Formpage.svelte";
  const firebaseConfig = {
    apiKey: "AIzaSyCzqllCOCHckcus9vqGAJiGrITeWPyeHwo",
    authDomain: "play-for-me-427f0.firebaseapp.com",
    projectId: "play-for-me-427f0",
    storageBucket: "play-for-me-427f0.appspot.com",
    messagingSenderId: "542373702374",
    appId: "1:542373702374:web:df426c78731bd665cf2927",
    measurementId: "G-789MM622JW",
  };
  const app = initializeApp(firebaseConfig);
  const auth = getAuth(app);
  export let text;
  export let userSignedIn;
  const provider = new GoogleAuthProvider();
  const signInWithGoogle = async () => {
    try {
      text = "Signing In....";
      await signInWithRedirect(auth, provider);
    } catch (error) {
      text = error.message;
    }
  };

  const signOutUser = async () => {
    text = "Signing Out....";
    try {
      await signOut(auth);
      text = "Signed Out";
      userSignedIn = false;
    } catch (error) {
      console.error("Error signing out:", error);
      text = "Error during sign out";
    }
  };
  let email = "";
  let password = "";

  const signInWithEmail = async () => {
    try {
      await signInWithEmailAndPassword(auth, email, password);
    } catch (error) {
      text = error.message;
    }
  };
</script>

<div class="container">
  <h1>{text}</h1>
  {#if !userSignedIn && text != "Access Denied"}
    <button
      on:click={() => {
        signInWithGoogle();
      }}>Google Sign In</button
    >
  {:else}
    <Formpage />
    <button
      on:click={() => {
        signOutUser();
      }}>Sign Out</button
    >
  {/if}
</div>

<style>
  .container button {
    background: rgb(255, 255, 255);
    border: 1px solid rgb(255, 255, 255);
    border-radius: 5px;
    padding: 10px;
    margin: 10px;
    cursor: pointer;
  }
  .container h1 {
    color: white;
    padding: 0 20px;
    text-align: center;
  }
  .container {
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
    height: 100vh;
    width: 100%;
    background: rgb(22, 24, 36);
  }
</style>
