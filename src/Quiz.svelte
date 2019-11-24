<script>
  let result = "";
  let correctAnswer = "b";

  function pickAnswer(answer) {
    if (answer === correctAnswer) {
      return (result = "Correct!");
    }
    result = "Oops";
  }
</script>

<div>
  {#if result}
    <h4>{result}</h4>
  {:else}
    <h4>Please select an answer</h4>
  {/if}
  <button on:click={() => pickAnswer('a')}>Answer A</button>
  <button on:click={() => pickAnswer('b')}>Answer B</button>
  <button on:click={() => pickAnswer('c')}>Answer C</button>
  <button on:click={() => pickAnswer('d')}>Answer D</button>
</div>
