<script>
  import Header from "./components/Header.svelte";
  import Footer from "./components/Footer.svelte";
  import PollList from "./components/PollList.svelte";
  import CreatePollForm from "./components/CreatePollForm.svelte";
  import Tabs from "./shared/Tabs.svelte";

  // tabs
  let items = ["Current Polls", "Add New Poll"];
  let activeTab = items[0];

  const handleTabChange = (e) => {
    activeTab = e.detail;
  };


  const handleAdd = (e) => {
    // const poll = e.detail;
    // polls = [poll, ...polls]; // not getting data now bcz store
    activeTab = items[0];
  };

	// const handleVote = (e) => {
	// 	const { id, option } = e.detail;

	// 	let copiedPolls = [...polls];
	// 	let upvotedPoll = copiedPolls.find(poll => poll.id === id);

	// 	if(option === 'a') {
	// 		upvotedPoll.votesA++;
	// 	} else if(option === 'b') {
	// 		upvotedPoll.votesB++;
	// 	} 

	// 	// find only gives a reference, therefore directly modifying the array
	// 	polls = copiedPolls;
	// }
</script>

<Header />
<main>
  <Tabs {activeTab} {items} on:tabChange={handleTabChange} />
  {#if activeTab === items[0]}
    <PollList />
  {:else if activeTab === items[1]}
    <CreatePollForm on:add={handleAdd} />
  {/if}
</main>

<Footer />

<style>
  main {
    max-width: 960px;
    margin: 40px auto;
  }
</style>
