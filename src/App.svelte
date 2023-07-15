<script>
  import { confettiAction } from "svelte-legos";
  const account = "HofRave";
  let amount = 0;

  $: href = amount
    ? `https://paypal.me/${account}/${amount}`
    : `https://paypal.me/${account}`;
</script>

<div />

<h1>Hofrave</h1>

<p>
  {#if amount}
    <big>{amount}€</big>
  {:else}
    <big>...€</big>
  {/if}
</p>

<section>
  {#each [2, 3, 5, 10] as donation}
    <button
      class:selected={donation === amount}
      on:click={() => (amount = donation)}>{donation}€</button
    >
  {/each}
  <button
    use:confettiAction
    class:selected={25 === amount}
    on:click={() => (amount = 25)}>25€</button
  >
</section>

<a {href} target="_blank" class:shine={!!amount}>Spenden</a>

<small>über Paypal</small>

<style>
  :global(body) {
    width: 100vw;
    height: 100dvh;

    margin: 0;
    display: flex;
    flex-flow: column;
    align-items: center;

  }

  div {
    position: absolute;
    inset: 0;
    background-image: url(/static/hero.webp);
    background-image: image-set(
      "/static/hero.avif" type("image/avif"),
      "/static/hero.webp" type("image/webp")
    );
    filter: blur(2px);
    -webkit-filter: blur(2px);
    background-position: center;
    background-size: cover;
    z-index: -1;
  }

  h1 {
    font-weight: bold;
    padding: 0 8px;
    font-size: 50px;
    text-transform: uppercase;
    border: 1px solid white;
  }

  button.selected {
    box-shadow: 0px 0px 0px 5px color(srgb 0.0668 0.446 0.9214);
  }

  button {
    font-size: 20px;
    padding: 2em;
    border-radius: 5px;
    background: white;
    cursor: pointer;
    font-weight: bold;
    border: 0;
    box-shadow: 0px 0px 3px 5px rgba(0, 0, 0, 0.3);
    color: black;
  }

  section {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 10px;
  }

  p {
    min-height: 2em;
  }

  big {
    font-size: 70px;
    font-family: myFirstFont;
  }

  a {
    background: color(srgb 0.0543 0.3027 0.7939);
    color: white;
    padding: 20px 50px;
    margin-top: 40px;
    border-radius: 25px;
    text-decoration: none;
    overflow: hidden;
    position: relative;
    font-weight: bold;
    box-shadow: 2px 2px 4px 2px rgba(0, 0, 0, 0.289);
  }

  a:not(.shine) {
    opacity: 0.6;
  }

  small {
    margin-top: 5px;
    opacity: 0.8;
  }

  a.shine:before {
    cursor: pointer;
    content: "";
    position: absolute;
    width: 100px;
    height: 100%;
    background-image: linear-gradient(
      120deg,
      rgba(255, 255, 255, 0) 30%,
      rgba(255, 255, 255, 0.8),
      rgba(255, 255, 255, 0) 70%
    );
    top: 0;
    left: -100px;
    animation: shine 2s infinite linear;
  }

  @keyframes shine {
    0% {
      left: -100px;
    }
    40% {
      left: 100%;
    }
    100% {
      left: 100%;
    }
  }
</style>
