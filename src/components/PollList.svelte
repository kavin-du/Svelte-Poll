<script>
// import { onDestroy, onMount } from 'svelte';

  import PollStore from '../store/PollStore.js';
  import PollDetails from "./PollDetails.svelte";

  /* 

  let polls = [];

  // whenever store changes this callback executes
  const unsubscribeThis = PollStore.subscribe(data => {
    polls = data;
  });


  onMount(() => {
    // get data from a db
    console.log('mounted...');
  });

  onDestroy(() => {
    // unsub from anything
    console.log('destroyed...');
    unsubscribeThis();
  });

  */



</script>
<!-- we directly access pollstore, so it will automatically 
unmounted, no need hooks -->
<div class="poll-list">
  {#each $PollStore as poll (poll.id)}
    <!-- forward the event to parent, bcz polldetails not nested in app.svelte -->
    <!-- <PollDetails {poll} on:vote /> no need to forward anymore bcz store -->
    <PollDetails {poll} />
  {/each}
</div>

<style>
  .poll-list {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;
  }
</style>
