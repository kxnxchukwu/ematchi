<script lang="ts">
  import Game from "./Game.svelte";
  import "../styles.css";
  import Modal from "./Modal.svelte";
  import { Levels } from "./levels";
  import { confetti } from "@neoconfetti/svelte";

  let state: "waiting" | "playing" | "paused" | "won" | "lost" = "waiting";
  let game: Game;
</script>

<svelte:head>
	<title>ematchi</title>
	<meta name="description" content="the emoji matching game" />

	<meta name="twitter:card" content="summary_large_image" />
	<meta property="twitter:domain" content="ematchi-game.vercel.app" />
	<meta property="twitter:url" content="https://ematchi-game.vercel.app" />
	<meta name="twitter:title" content="ematchi" />
	<meta name="twitter:description" content="the emoji matching game" />
	<meta name="twitter:image" content="https://ematchi.vercel.app/og.png" />
</svelte:head>

<main>
<Game
  on:play={() => {
    state = "playing";
  }}
  on:pause={() => {
    state = "paused";
  }}
  on:win={() => {
    state = "won";
  }}
  on:lose={() => {
    state = "lost";
  }}
  bind:this={game}
/>

{#if state !== "playing"}
  <Modal>
    <header>
      <h1>e<span>match</span>i</h1>
      <p>the emoji matching game</p>
    </header>
    {#if state === "won" || state === "lost"}
      <p>you {state} the game!</p>
    {:else if state === "paused"}
      <p>game paused</p>
    {:else if state === "waiting"}
      <p>Choose a level:</p>
    {/if}

    <div class="buttons">
      {#if state === "paused"}
					<button on:click={() => game.resume()}>resume</button>
					<button on:click={() => (state = 'waiting')}> quit </button>
      {:else}
        {#each Levels as level}
          <button
            on:click={() => {
              game.start(level);
            }}>{level.label}</button
          >
        {/each}
      {/if}
    </div>
  </Modal>
{/if}

{#if state === "won"}
  <div
    class="confetti"
    use:confetti={{
      stageHeight: innerHeight,
      stageWidth: innerWidth,
    }}
  ></div>
{/if}
</main>

<style>
  	main {
		text-align: center;
		height: 100%;
		display: flex;
		flex-direction: column;
		justify-content: center;
	}

	header {
		font-size: min(5vw, 2rem);
		font-family: Grandstander;
	}
  h1 {
    font-size: 4em;
  }
  h1 span {
    color: purple;
  }

  p {
    font-family: Grandstander;
  }
  .confetti {
    position: fixed;
    width: 100%;
    height: 100%;
    left: 50%;
    top: 30%;
    pointer-events: none;
  }
  button{
    background:purple;
    color: #fff;
    font-size: inherit;
    font-family: inherit;
    border: none;
    padding: 1em;
    border-radius: 0.5em;
    margin:10px
  }
</style>
