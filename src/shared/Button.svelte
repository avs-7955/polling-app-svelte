<script>
	export let type = "primary"
	export let flat = false
	export let inverse = false
</script>

<button class={type} class:flat class:inverse on:click>
	<slot />
</button>

<style>
	button {
		border: 0;
		cursor: pointer;
		padding: 8px 12px;
		border-radius: 6px;
		font-weight: bold;
		box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.2);
	}
	.primary {
		background-color: #d91b42;
		color: white;
	}
	.secondary {
		/* background-color: #45c496; */
		background-color: #ffd782;
		color: white;
	}
	.flat {
		box-shadow: none;
	}
	.primary:hover {
		color: #d91b42;
		background-color: white;
		border: 2px solid #d91b42;
	}
	.secondary:hover {
		/* color: #45c496; */
		color: #ffd782;
		background-color: white;
		/* border: 2px solid #45c496; */
		border: 2px solid #ffd782;
	}
	.primary.inverse {
		color: #d91b42;
		background-color: white;
		border: 2px solid #d91b42;
	}
	.secondary.inverse {
		/* color: #45c496; */
		color: #ffd782;
		background-color: white;
		border: 2px solid #ffd782;
	}
</style>
