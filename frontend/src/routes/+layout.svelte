<script lang="ts">
  import { onMount } from "svelte";

  function handleOnClick(route: string, type = "normal") {
    if (type === "normal") {
      window.location.href = route;
    } else if (type === "help") {
      window.open(route, "_blank");
    }
  }
  let path = "";
  onMount(() => {
    if (typeof window !== "undefined") {
      path = window.location.pathname.split("/")[1];
      console.log("🍷 ~ window.location.pathname:", window.location.pathname.split("/")[1]);
    }
  });
</script>

<div class="app">
  <header>
    <div>
      <img
        style="margin-right: 10px;"
        src="/markdown.png"
        height="35"
        width="35"
        alt="markdown"
      />
      <h2><a href="https://github.com/skar-software/pubdeskmd" target="_blank">Pubdeskmd</a></h2>
    </div>
    <div>
      <button
        class:current-page={path === "login"}
        class="header-button"
        on:click={() => handleOnClick("/login")}
      >
        Connect
      </button>

      |
      <button
        class:current-page={path === "repos"}
        class="header-button"
        on:click={() => handleOnClick("/repos")}>Repos</button
      >
      |
      <!-- <button
        class="header-button"
        on:click={() => handleOnClick("/repos")}>Markdown Editor</button
      >
      | -->
      <button
        class="header-button"
        on:click={() => handleOnClick("https://skar-software.github.io/pubdeskmd", "help")}>Help</button
      >
    </div>
  </header>
  <main>
    <slot />
  </main>
  <div class="footer-margin"></div>
  <footer>
    <span style="font-weight: 400;">
      Powered by:
      <a
        class="foot"
        href="https://github.com/BearToCode/carta"
        >Carta Markdown Editor
      </a>
    </span>
  </footer>
</div>

<style>
  div {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: flex-start;
    font-size: normal;
  }
  a{
    color: #415a77;
  }
  h2 {
    color: #415a77;
    text-decoration: underline;
    font-size: 1.5em;
    margin-top: 0;
    font-weight: 600;
    text-align: center;
    /* padding-right: 30vw; */
    text-decoration-color: red;
  }
  header {
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    align-items: flex-start;
    padding: 10px;
    width: 100%;
    background-color: #edede9;
  }
  * {
    font-family: poppins;
  }
  .app {
    display: flex;
    flex-direction: column;
    background-color: #edede9;
    /* min-height: 100vh; */
  }

  main {
    margin: 0;
    padding: 0;
    width: 100%;
  }
  .foot,
  span {
    font-weight: 700;
    font-size: 1rem;
  }
  .footer-margin {
    margin: 40px;
  }
  footer {
    overflow-x: hidden;
    position: fixed;
    bottom: 0%;
    width: 100vw;
    background: #778da9;
    color: aliceblue;
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    align-items: center;
  }

  footer a {
    font-weight: bold;
    color: aliceblue;
    text-decoration-color: aliceblue;
  }

  @media (min-width: 480px) {
    footer {
      padding: 12px 0;
    }
  }
  .header-button {
    background-color: transparent;
    outline: none;
    border: none;
    font-size: 1rem;
    color: #415a77;
    font-weight: 600;
    padding: 0 10px;
    cursor: pointer;
  }
  .header-button:hover {
    text-decoration: underline;
    text-decoration-color: #ff3e00;
  }
  .current-page {
    text-decoration: underline;
    text-decoration-color: #ff3e00;
    font-weight: 700 !important;
    cursor: pointer;
  }
</style>
