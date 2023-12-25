<script>
  import Sidebar from "./components/Sidebar.svelte";
  import Home from "./components/Home.svelte";
  import Contact from "./components/Contact.svelte";
  import Show from "./components/Show.svelte";
  import { initializeApp } from "firebase/app";
  import { getAuth, onAuthStateChanged } from "firebase/auth";
  import { getFirestore, doc, getDoc } from "firebase/firestore";

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
  const db = getFirestore(app);
  let text = "Loading....";
  let userSignedIn = false;
  let isLoading = true;
  let currentTab;
  let unsubscribe;
  function changeTab(event) {
    currentTab = event.detail;
  }

  unsubscribe = onAuthStateChanged(auth, (user) => {
    if (user) {
      const uid = user.uid;
      const docRef = doc(db, "users", uid);
      getDoc(docRef)
        .then((docSnap) => {
          const userData = docSnap.data();
          text = `Welcome! ${userData.name}`;
        })
        .catch((error) => {
          console.error("Error getting document:", error);
          text = "User not elligible to Join/Host a Show";
        });
      userSignedIn = true;
      currentTab = "Shows";
    } else {
      if (currentTab != "Shows") {
        currentTab = "Home";
      }
      userSignedIn = false;
      text = "Sign In to Join/Host a Show";
    }
    isLoading = false;
  });
</script>

<main>
  {#if isLoading}
    <h1
      style="
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        color: #fff;
      "
    >
      Loading...
    </h1>
  {:else}
    <Sidebar {currentTab} on:ChangeTab={changeTab} />

    {#if currentTab == "Home"}
      <Home
        on:click={() => {
          currentTab = "Contact";
        }}
      />
    {:else if currentTab == "Contact"}
      <Contact
        on:click={() => {
          currentTab = "Home";
        }}
      />
    {:else if currentTab == "Shows"}
      <Show {text} {userSignedIn} />
    {/if}{/if}
</main>

<style>
</style>
