<script>
	import Header from './components/Header.svelte';
	import Footer from './components/Footer.svelte';
	import CreatePollForm from './components/CreatePollForm.svelte';
	import Tabs from './shared/Tabs.svelte';

	// tabs
	let items = ['Current Polls', 'Add New Poll'];
	let activeTab = items[1];


	const handleTabChange = (e) => {
		activeTab = e.detail;
	}
</script>

<Header />
<main>
	<Tabs {activeTab} {items} on:tabChange={handleTabChange} />
	{#if activeTab === items[0]}
	<p>shit is not real</p>
	{:else if activeTab === items[1]}
		<CreatePollForm />
	{/if}
</main>

<Footer />

<style>
	main {
		max-width: 960px;
		margin: 40px auto;
	}
</style>