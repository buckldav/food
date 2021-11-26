<script>
  export let foodOptions;
  const DAYS_INIT = 5;
  let days = DAYS_INIT;
  let generated = JSON.parse(localStorage.getItem("generated"));
  generated = generated ? generated : [];
  let groceryList = JSON.parse(localStorage.getItem("grocery"));
  let usedFoods = [];

  /**
   * Generates food list. If foodOptions < days, food will be reused, else food in list will be unique.
   * @param e
   */
  const generateFoodList = (e) => {
    e.preventDefault();
    generated = [];
    while (generated.length < days) {
      if (usedFoods.length === foodOptions.length) usedFoods = [];
      const rando = foodOptions[Math.floor(Math.random() * foodOptions.length)];
      if (!usedFoods.includes(rando)) {
        generated.push(rando);
        usedFoods.push(rando);
      }
    }
    localStorage.setItem("generated", JSON.stringify(generated));
  };

  function handleGroceryList(e) {
    localStorage.setItem("grocery", JSON.stringify(e.target.value));
    groceryList = e.target.value;
  }

  function handleClearAll(e) {
    if (window.confirm("Are you sure?")) {
      localStorage.removeItem("generated");
      localStorage.removeItem("grocery");
      days = DAYS_INIT;
      window.location.reload();
    }
  }
</script>

<main>
  <h1>Food</h1>

  <form on:submit={generateFoodList}>
    <input
      aria-label="Number of days of food"
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

  <ol>
    {#each generated as g}
      <li>{g}</li>
    {/each}
  </ol>

  {#if generated.length > 1}
    <label for="grocery">Grocery List</label>
    <textarea
      id="grocery"
      rows="4"
      on:input={handleGroceryList}
      bind:value={groceryList}
    />
    <br />
    <button on:click={handleClearAll}>Clear All</button>
  {/if}
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

  label {
    margin-top: 1em;
    font-weight: bold;
  }

  ol {
    text-align: start;
    margin: 0.5em auto;
    padding-left: 1em;
    width: fit-content;
  }
</style>
