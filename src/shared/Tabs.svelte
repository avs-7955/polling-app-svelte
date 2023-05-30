<script>
	import { createEventDispatcher } from "svelte"

	export let items
	export let currentActive
	const dispatch = createEventDispatcher()
</script>

<div class="tabs">
	<ul>
		{#each items as item}
			<!-- svelte-ignore a11y-click-events-have-key-events -->
			<li on:click={() => dispatch("tabChange", item)}>
				<div class:active={item === currentActive}>{item}</div>
			</li>
		{/each}
	</ul>
</div>

<style>
	.tabs {
		margin-bottom: 40px;
	}
	ul {
		list-style-type: none;
		display: flex;
		justify-content: center;
		padding: 0;
	}
	li {
		margin: 0 16px;
		font-size: 18px;
		cursor: pointer;
		color: #555;
	}
	.active {
		padding-bottom: 8px;
		border-bottom: 2px solid #d91b42;
		color: #d91b42;
	}
</style>
