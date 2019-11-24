<script>
  function pickAnswer() {
    console.log("answered");
  }
</script>

<div>
  <button on:click={pickAnswer}>Answer A</button>
  <button on:click={pickAnswer}>Answer B</button>
  <button on:click={pickAnswer}>Answer C</button>
  <button on:click={pickAnswer}>Answer D</button>
</div>
