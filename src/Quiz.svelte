<script>
  import { fade, blur, fly, slide, scale } from "svelte/transition";
  import Question from "./Question.svelte";

  let activeQuestion = 0;
  let score = 0;
  let quiz = getQuiz();

  async function getQuiz() {
    const res = await fetch(
      "https://opentdb.com/api.php?amount=10&category=12&type=multiple"
    );
    const quiz = await res.json();
    return quiz;
  }

  function nextQuestion() {
    activeQuestion += 1;
  }

  function resetQuiz() {
    score = 0;
    activeQuestion = 0;
    quiz = getQuiz();
  }

  function addToScore() {
    score += 1;
  }

  //Reactive statement
  $: if (score > 1) {
    alert("you won!");
    resetQuiz();
  }
  $: questionNumber = activeQuestion + 1;
</script>

<style>
  .fade-wrapper {
    position: absolute;
  }
</style>

<div>
  <button on:click={resetQuiz}>Start new Quiz</button>

  <h3>My Score: {score}</h3>
  <h4>Question: #{questionNumber}</h4>

  {#await quiz}
    Loading....
  {:then data}
    {#each data.results as question, index}
      {#if index === activeQuestion}
        <div transition:blur={{ amount: 10 }} class="fade-wrapper">
          <Question {addToScore} {nextQuestion} {question} />
        </div>
      {/if}
    {/each}
  {/await}
</div>
