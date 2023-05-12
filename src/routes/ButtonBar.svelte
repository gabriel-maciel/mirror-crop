<script>
	export let buttons = [];
</script>

<div class="button-bar">
	{#each buttons as button}
		<button>
			<i class="material-icons">{button.icon}</i>
		</button>
	{/each}
</div>

<style>
	.button-bar {
		display: flex;
		gap: 10px;
		margin-bottom: 10px;
	}

	button {
		padding: 5px;
	}
</style>
