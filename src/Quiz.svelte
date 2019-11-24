<script>
  let result = "";
  let correctAnswer = "b";
  let answers = ["a", "b", "c", "d"];

  function pickAnswer(answer) {
    if (answer === correctAnswer) {
      return (result = "Correct!");
    }
    result = "Oops";
  }
</script>

<style>
  :global(h4) {
    color: red;
  }
</style>

<div>
  {#if result}
    <h4>{result}</h4>
  {:else}
    <h4>Please select an answer</h4>
  {/if}
  {#each answers as answer}
    <button on:click={() => pickAnswer(answer)}>
      Answer {answer.toUpperCase()}
    </button>
  {/each}
</div>
