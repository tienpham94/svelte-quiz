<script>
  export let question;

  let isCorrect;
  let isAnswered = false;
  let answers = question.incorrect_answers.map(answer => ({
    answer,
    correct: false
  }));

  let allAnswers = [
    ...answers,
    {
      answer: question.correct_answer,
      correct: true
    }
  ];

  shuffle(allAnswers);

  function shuffle(array) {
    array.sort(() => Math.random() - 0.5);
  }

  function checkQuestion(correct) {
    isAnswered = true;
    isCorrect = correct;
  }
</script>

<h3>
  {@html question.question}
</h3>

{#if isAnswered}
  <h4>
    {#if isCorrect}You got it right{:else}You goofed up{/if}

  </h4>
{/if}

{#each allAnswers as answer}
  <button on:click={() => checkQuestion(answer.correct)}>
    {@html answer.answer}
  </button>
{/each}
