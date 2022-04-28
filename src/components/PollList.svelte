<script>
  // these only works on plain html elements, not custom elements
  // transitions controls how element enter or delete from dom
  import { fade, scale} from 'svelte/transition';
  import {flip} from 'svelte/animate';
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

 <!-- forward the event to parent, bcz polldetails not nested in app.svelte -->
  <!-- <PollDetails {poll} on:vote /> no need to forward anymore bcz store -->
  <!-- local means animate only individual element removed from dom -->
    
<!-- animate:flip -> animate when the order of "each" block changes -->
<div class="poll-list">
  {#each $PollStore as poll (poll.id)}
   <div in:fade out:scale|local animate:flip={{duration: 500}}>
      <PollDetails {poll}/>
    </div>
  {/each}
</div>

<style>
  .poll-list {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;
  }
</style>
