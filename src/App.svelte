<script>
	import Header from "./components/Header.svelte"
	import Footer from "./components/Footer.svelte"
	import Tabs from "./shared/Tabs.svelte"
	import CreatePollForm from "./components/CreatePollForm.svelte"
	import PollList from "./components/PollList.svelte"

	//tabs
	let items = ["Current Polls", "Add New Poll"]
	let currentActive = "Current Polls"

	const handleTabChange = (e) => {
		currentActive = e.detail
	}

	const handleAddPoll = (e) => {
		currentActive = "Current Polls"
	}

	const handleAddVote = (e) => {}
</script>

<Header />
<main>
	<Tabs {items} {currentActive} on:tabChange={handleTabChange} />
	{#if currentActive === "Current Polls"}
		<!-- <p>Current polls component comes here.</p> -->
		<PollList />
	{:else if currentActive === "Add New Poll"}
		<!-- <p>Add new poll component comes here.</p> -->
		<CreatePollForm on:addPoll={handleAddPoll} />
	{/if}
</main>
<Footer />

<style>
	main {
		max-width: 960px;
		margin: 40px auto;
	}
</style>
