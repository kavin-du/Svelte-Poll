<script>
  import Card from "../shared/Card.svelte";
  import PollStore from '../store/PollStore';
  import Button from "../shared/Button.svelte";
  import { tweened } from 'svelte/motion';
  // import {createEventDispatcher} from 'svelte';

  // const dispatch = createEventDispatcher();
  export let poll;

  // reactive values
  $: totalVotes = poll.votesA + poll.votesB;
  $: percentA = Math.floor((poll.votesA/totalVotes) * 100) || 0; // handling division by zero when animating
  $: percentB = Math.floor((poll.votesB/totalVotes) * 100) || 0;

  // tweend percentages 
  const tweenedA = tweened(0); // initial values of tween
  const tweenedB = tweened(0);
  $: tweenedA.set(percentA);
  $: tweenedB.set(percentB);


  const handleVotes = (option, id) => {
    // dispatch('vote', { option, id });

    PollStore.update(currPolls => {

      let copiedPolls = [...currPolls];
      let upvotedPoll = copiedPolls.find(poll => poll.id === id);
  
      if(option === 'a') {
        upvotedPoll.votesA++;
      } else if(option === 'b') {
        upvotedPoll.votesB++;
      } 
  
      // find only gives a reference, therefore directly modifying the array
      return copiedPolls;
    });
  }

  const handleDelete = (id) => {
    PollStore.update(currPolls => {
      return currPolls.filter(poll => poll.id !== id);
    });
  }
</script>

<Card>
  <div class="poll">
    <h3>{poll.question}</h3>
    <p>Total votes: {totalVotes}</p>
    <div class="answer" on:click={() => handleVotes('a', poll.id)}>
      <!-- subscribing to non reactive value -->
      <div class="percent percent-a" style="width: {$tweenedA}%" />
      <span>{poll.answerA} ({poll.votesA})</span>
    </div>

    <div class="answer" on:click={() => handleVotes('b', poll.id)}>
      <div class="percent percent-b" style="width: {$tweenedB}%" />
      <span>{poll.answerB} ({poll.votesB})</span>
    </div>
    <div class="delete">
      <Button flat={true} on:click={() => handleDelete(poll.id)}>Delete</Button>
    </div>
  </div>
</Card>

<style>
  h3 {
    margin: 0 auto;
    color: #555;
  }
  p {
    margin-top: 6px;
    font-size: 14px;
    color: #aaa;
    margin-bottom: 30px;
  }
  .answer {
    background: #fafafa;
    cursor: pointer;
    margin: 10px auto;
    position: relative;
  }
  .answer:hover {
    opacity: 0.6;
  }
  span {
    display: inline-block;
    padding: 10px 20px;
  }
  .percent {
    height: 100%;
    position: absolute; /* top left 0,0 */
    box-sizing: border-box;
  }
  .percent-a {
    border-left: 4px solid #d91b42;
    background: rgba(217,27,66,0.2);
  }
  .percent-b {
    border-left: 4px solid #45c496;
    background: rgba(69,196,150,0.2);
  }
  .delete {
    margin-top: 30px;
    text-align: center;
  }
</style>
