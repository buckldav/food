<script>
  import Edit from "svelte-icons/fa/FaEdit.svelte";
  import Hamburger from "svelte-icons/fa/FaHamburger.svelte";
  import InfoCircle from "svelte-icons/fa/FaInfoCircle.svelte";
  import Generator from "./Generator.svelte";
  import List from "./List.svelte";
  import Info from "./Info.svelte";

  export let foodOptions = JSON.parse(localStorage.getItem("foodOptions"));
  foodOptions = foodOptions ? foodOptions : [];

  function handleCreate(event) {
    if (event.detail.food) {
      foodOptions = [...foodOptions, event.detail.food].sort((a, b) =>
        a > b ? 1 : -1
      );
      localStorage.setItem("foodOptions", JSON.stringify(foodOptions));
    }
  }

  function handleDestroy(event) {
    foodOptions = foodOptions.filter((i) => i !== event.detail.food);
    localStorage.setItem("foodOptions", JSON.stringify(foodOptions));
  }

  let currentTab = 1;
</script>

{#if currentTab === 0}
  <List {foodOptions} on:create={handleCreate} on:destroy={handleDestroy} />
{/if}
{#if currentTab === 1}
  <Generator {foodOptions} />
{/if}
{#if currentTab === 2}
  <Info />
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
