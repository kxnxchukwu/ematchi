<script lang="ts">
  import { send } from "./transitions";
  import { get_twemoji_url } from "./utils";

  export let emoji: string;
  export let selected: boolean;
  export let found: boolean;
  export let group: "a" | "b";
</script>

<div class="square" class:flipped={selected || found}>
  <button on:click />
  <div class="background" />
  {#if !found}
    <img
      out:send={{ key: `${emoji}:${group}` }}
      alt={emoji}
      src={get_twemoji_url(emoji)}
    />
  {/if}
</div>

<style>
  .square {
    display: flex;
    width: 100%;
    height: 100%;
    justify-content: center;
    align-items: center;
    transition: filter 0.4s;
    transform-style: preserve-3d;
    transform: rotateY("180deg");
    transition: transform 0.4s;
  }
  .flipped {
    transform: rotateY(180deg);
  }
  button {
    position: absolute;
    width: 100%;
    height: 100%;
    backface-visibility: hidden;
    background: #eee;
    border: 0;
    border-radius: 1em;
  }
  .background {
    position: absolute;
    background: white;
    border: 0.5rem solid #eee;
    border-radius: 1em;
    font-size: inherit;
    transform: rotateY(180deg);
    backface-visibility: hidden;
    width: 100%;
    height: 100%;
  }
  img {
    width: 8em;
    height: 8em;
    pointer-events: none;
    transform: rotateY(180deg);
    backface-visibility: hidden;
  }
</style>
