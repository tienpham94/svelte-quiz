<script>
  import Question from "./Question";

  let quiz = getQuiz();

  async function getQuiz() {
    const res = await fetch(
      "https://opentdb.com/api.php?amount=10&category=12&type=multiple"
    );
    const quiz = await res.json();
    return quiz;
  }

  function handleClick() {
    quiz = getQuiz();
  }
</script>

<style>
  :global(h4) {
    color: red;
  }
</style>

<div>
  <button on:click={handleClick}>Get Questions</button>

  {#await quiz}
    Loading....
  {:then data}
    {#each data.results as question}
      <Question {question} />
    {/each}
  {/await}
</div>
