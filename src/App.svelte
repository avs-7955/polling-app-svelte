<script>
	import Header from "./components/Header.svelte"
	import Footer from "./components/Footer.svelte"
	import Tabs from "./shared/Tabs.svelte"
	import CreatePollForm from "./components/CreatePollForm.svelte"

	let items = ["Current Polls", "Add New Poll"]
	let currentActive = "Current Polls"

	const handleTabChange = (e) => {
		currentActive = e.detail
	}
</script>

<Header />
<main>
	<Tabs {items} {currentActive} on:tabChange={handleTabChange} />
	{#if currentActive === "Current Polls"}
		<p>Current polls component comes here.</p>
	{:else if currentActive === "Add New Poll"}
		<!-- <p>Add new poll component comes here.</p> -->
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
