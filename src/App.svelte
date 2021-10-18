<script>
  import Edit from "svelte-icons/fa/FaEdit.svelte";
  import Hamburger from "svelte-icons/fa/FaHamburger.svelte";
  import InfoCircle from "svelte-icons/fa/FaInfoCircle.svelte";
  import Generator from "./Generator.svelte";
  import List from "./List.svelte";

  export const foodOptions = [
    "Tostadas",
    "Hawaiian haystacks",
    "Spaghetti",
    "Enchiladas",
    "Mandarin chicken salad",
    "Cincinnati chili",
    "Pasta salad",
    "Pizza",
    "Stir fry",
    "Mashed potato bowls",
    "Breakfast",
    "Noodle casserole",
    "Tacos",
    "Hot dogs",
    "Sliders",
    "Beef and Broccoli",
    "Soup",
    "Sandwiches of various kinds",
    "Fajitas/burritos",
    "Garlic chicken",
  ];

  let currentTab = 1;
</script>

{#if currentTab === 0}
  <List {foodOptions} />
{/if}
{#if currentTab === 1}
  <Generator {foodOptions} />
{/if}
{#if currentTab === 2}
  <List {foodOptions} />
{/if}

<footer>
  <nav>
    <button on:click={() => (currentTab = 0)}>
      <div class="icon"><Edit /></div>
      Edit Foods
    </button>
    <button on:click={() => (currentTab = 1)}>
      <div class="icon"><Hamburger /></div>
      Generate Foods
    </button>
    <button on:click={() => (currentTab = 2)}>
      <div class="icon"><InfoCircle /></div>
      What is Food?
    </button>
  </nav>
</footer>

<style>
  footer nav {
    display: flex;
    justify-content: space-evenly;
  }

  footer nav button {
    background: transparent;
    font-size: 0.625em;
    text-align: center;
  }

  footer nav button .icon {
    height: 36px;
    padding-bottom: 4px;
    margin: 0 auto;
  }
</style>
