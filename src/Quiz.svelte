<script>
  export let quizName = "Tien Quiz";

  let a = 0;
  let b = 0;
</script>

<div>
  <h2>{quizName}</h2>
  <input bind:value={a} type="number" />
  <input bind:value={b} type="number" />
  <h4>{a + b}</h4>
</div>
