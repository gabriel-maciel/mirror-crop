<script>
	import Header from './Header.svelte';
	import ImagePanel from './ImagePanel.svelte';
	import './styles.css';
</script>

<div class="app">
	<div class="container">
		<Header />
		<ImagePanel />
	</div>
</div>

<style>
	.app {
		display: flex;
		justify-content: center;
		align-items: center;
		min-height: 100vh;
		margin: 0;
		background: linear-gradient(to bottom, #d8f3dc, #ffffff);
		font-family: Arial, sans-serif;
	}

	.container {
		display: flex;
		flex-direction: column;
		max-width: 56rem;
		width: 100%;
		box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
		border-radius: 10px;
		overflow: hidden;
	}
</style>
