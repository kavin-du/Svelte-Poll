<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();
  export let items;
  export let activeTab;
</script>

<div class="tabs">
  <ul>
    {#each items as tab}
      <li on:click={() => dispatch('tabChange', tab)}>
        <div class:active={tab === activeTab}>{tab}</div>
      </li>
    {/each}
  </ul>
</div>

<style>
  .tabs {
    margin-bottom: 40px;
  }
  li {
    margin: 0 16px;
    font-size: 18px;
    color: #555;
    cursor: pointer;
  }
  ul {
    display: flex;
    justify-content: center;
    padding: 0;
    list-style-type: none;
  }
  .active {
    color: tomato;
    border-bottom: 2px solid tomato;
    padding-bottom: 8px;
  }
</style>
