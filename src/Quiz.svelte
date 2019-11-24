<script>
  import Question from "./Question.svelte";

  let activeQuestion = 1;
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

<div>
  <button on:click={handleClick}>Start new Quiz</button>

  <h3>My Score: 0</h3>

  {#await quiz}
    Loading....
  {:then data}
    {#each data.results as question, index}
      {#if index === activeQuestion}
        <Question {question} />
      {/if}
    {/each}
  {/await}
</div>
