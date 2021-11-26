<script>
  export let foodOptions;

  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  function create(event) {
    let food = prompt("Name of Food:", "");
    dispatch("create", { food });
  }

  function destroy(event) {
    dispatch("destroy", {
      food: event.target.name,
    });
  }
</script>

<header>
  <button on:click={create}> + Add New Food </button>
</header>

<main>
  {#if foodOptions.length === 0}
    <p>Welcome to FOOD! Add foods here to begin.</p>
  {/if}

  <table>
    {#each foodOptions as food}
      <tr>
        <td>
          <button on:click={destroy} name={food} aria-label="delete">
            &ndash;
            <!-- <div class="icon"><MinusSquare /></div> -->
          </button>
        </td>
        <td>{food}</td>
      </tr>
    {/each}
    <tr>
      <td />
    </tr>
  </table>
</main>

<style>
  header {
    display: flex;
    justify-content: center;
  }

  main {
    max-height: calc(100vh - 156px);
  }

  table {
    text-align: left;
  }

  td {
    display: inline-flex;
    align-items: center;
    margin: 0.25em 0;
  }

  td button {
    margin: 0 0.5em 0 0;
    background: transparent;
    padding: 0 0.5em;
    font-weight: bolder;
    color: var(--green);
  }
</style>
