<script>
  export let foodOptions;
  export function changeTab() {}
  let days = 5;
  let generated = [];

  /**
   * Generates food list. If foodOptions < days, food will be reused, else food in list will be unique.
   * @param e
   */
  const generateFoodList = (e) => {
    e.preventDefault();
    generated = [];
    let usedFoods = [];
    while (generated.length < days) {
      if (usedFoods.length === foodOptions.length) usedFoods = [];
      const rando = foodOptions[Math.floor(Math.random() * foodOptions.length)];
      if (!usedFoods.includes(rando)) {
        generated.push(rando);
        usedFoods.push(rando);
      }
    }
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
    <button type="submit" disabled={!foodOptions.length}>Gimme Food</button>
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
