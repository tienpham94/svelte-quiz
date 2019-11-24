<script>

</script>

<style>
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

<div class="modal-bg">
  <div class="modal">
    <button>Close</button>
    <slot />
  </div>
</div>
