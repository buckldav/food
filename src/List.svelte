<script>
  export let foodOptions;
  import MinusSquare from "svelte-icons/fa/FaMinusSquare.svelte";
</script>

<main>
  <button>+ Add New Food</button>
  <table>
    {#each foodOptions as food}
      <tr>
        <td><button><div class="icon"><MinusSquare /></div></button></td>
        <td>{food}</td>
      </tr>
    {/each}
    <tr>
      <td />
    </tr>
  </table>
</main>

<style>
  table {
    text-align: left;
  }
  td {
    display: inline-flex;
    align-items: center;
  }
  td button {
    margin: 0;
    background: transparent;
  }

  td button div {
    height: 1em;
  }
</style>
