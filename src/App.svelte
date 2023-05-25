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

	// polls
	let polls = [
		{
			id: 1,
			question: "Python or JavaScript?",
			answerA: "Python",
			answerB: "JavaScript",
			votesA: 9,
			votesB: 15,
		},
	]

	const handleAddPoll = (e) => {
		let poll = e.detail
		polls = [poll, ...polls]
		console.log(polls)
		currentActive = "Current Polls"
	}

	const handleAddVote = (e) => {
		let option = e.detail.option
		let id = e.detail.id
		let copiedPolls = [...polls]
		let upvotedPoll = copiedPolls.find((poll) => poll.id === id)
		if (option == "a") upvotedPoll.votesA += 1
		if (option == "b") upvotedPoll.votesB += 1

		polls = copiedPolls
	}
</script>

<Header />
<main>
	<Tabs {items} {currentActive} on:tabChange={handleTabChange} />
	{#if currentActive === "Current Polls"}
		<!-- <p>Current polls component comes here.</p> -->
		<PollList {polls} on:incVote={handleAddVote} />
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
