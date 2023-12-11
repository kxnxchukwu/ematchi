<div class="modal-background">
  <slot />
</div>

<style>
  .modal-background {
    position: fixed;
    width: 100%;
    height: 100%;
    left: 0;
    top: 0;
    display: grid;
    place-items: center;
    backdrop-filter: blur(10px);
    z-index: 999;
    transition: all .2s;
    text-align:center
  }
</style>
