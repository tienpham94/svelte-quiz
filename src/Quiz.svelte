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
  <h4>{result}</h4>
  <button on:click={() => pickAnswer('a')}>Answer A</button>
  <button on:click={() => pickAnswer('b')}>Answer B</button>
  <button on:click={() => pickAnswer('c')}>Answer C</button>
  <button on:click={() => pickAnswer('d')}>Answer D</button>
</div>
