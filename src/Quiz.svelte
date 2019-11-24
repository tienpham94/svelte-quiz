<script>
  import { fade, blur, fly, slide, scale } from "svelte/transition";
  import { onMount, beforeUpdate, afterUpdate, onDestroy } from "svelte";
  import Question from "./Question.svelte";
  import Modal from "./Modal.svelte";
  import { score } from "./store.js";

  let activeQuestion = 0;
  let quiz = getQuiz();
  let isModalOpen = false;

  async function getQuiz() {
    const res = await fetch(
      "https://opentdb.com/api.php?amount=10&category=12&type=multiple"
    );
    const quiz = await res.json();
    return quiz;
  }

  onMount(() => console.log("mounted"));
  beforeUpdate(() => console.log("1"));
  afterUpdate(() => console.log("2"));
  onDestroy(() => console.log("3"));

  function nextQuestion() {
    activeQuestion += 1;
  }

  function resetQuiz() {
    isModalOpen = false;
    score.set(0);
    activeQuestion = 0;
    quiz = getQuiz();
  }

  //Reactive statement
  $: if ($score > 0) {
    isModalOpen = true;
  }
  $: questionNumber = activeQuestion + 1;
</script>

<style>
  .fade-wrapper {
    position: absolute;
  }
</style>

<div>
  <button on:click|once={resetQuiz}>Start new Quiz</button>

  <h3>My Score: {$score}</h3>
  <h4>Question: #{questionNumber}</h4>

  {#await quiz}
    Loading....
  {:then data}
    {#each data.results as question, index}
      {#if index === activeQuestion}
        <div transition:blur={{ amount: 10 }} class="fade-wrapper">
          <Question {nextQuestion} {question} />
        </div>
      {/if}
    {/each}
  {/await}
</div>

{#if isModalOpen}
  <Modal on:close={resetQuiz}>
    <h2>You won!</h2>
    <p>Congrats!</p>
    <button on:click={resetQuiz}>Start over</button>
  </Modal>
{/if}
