<script>
  export let foodOptions;
  let days = 4;
  let generated = [];

  const generateFoodList = (e) => {
    e.preventDefault();
    generated = [];
    while (generated.length < days) {
      const rando = foodOptions[Math.floor(Math.random() * foodOptions.length)];
      if (!generated.includes(rando)) generated.push(rando);
    }
    console.log(generated);
  };
</script>

<main>
  <h1>Food</h1>

  <form on:submit={generateFoodList}>
    <input
      type="number"
      min="1"
      max="10"
      value={days}
      on:change={(e) => {
        days = e.target.value;
      }}
    />
    <button type="submit">Gimme Food</button>
  </form>

  <ul>
    {#each generated as g}
      <li>{g}</li>
    {/each}
  </ul>
</main>

<style>
  input {
    width: 80px;
  }
  /* ensures the increment/decrement arrows always display */
  input[type="number"]::-webkit-inner-spin-button,
  input[type="number"]::-webkit-outer-spin-button {
    opacity: 1;
  }
</style>
