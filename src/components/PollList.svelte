<script>
  import PollDetails from "./PollDetails.svelte";

  export let polls = [];
</script>

<div class="poll-list">
  {#each polls as poll (poll.id)}
    <!-- forward the event to parent, bcz polldetails not nested in app.svelte -->
    <PollDetails {poll} on:vote />
  {/each}
</div>

<style>
  .poll-list {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;
  }
</style>
