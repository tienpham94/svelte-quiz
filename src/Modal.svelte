<script>
  import { fade, blur, fly, slide, scale } from "svelte/transition";
  import { createEventDispatcher } from "svelte";

  let w;
  const dispatch = createEventDispatcher();
</script>

<style lang="scss">
  .modal-bg {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.8);
  }
  .modal {
    background: white;
    padding: 20px;
  }
</style>

<div class="modal-bg" transition:fade>
  <div class="modal" transition:fly={{ y: -100 }} bind:clientWidth={w}>
    <button on:click={() => dispatch('close')}>Close</button>
    {w}
    <slot />
  </div>
</div>
