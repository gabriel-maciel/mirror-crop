<script>
	import ButtonBar from './ButtonBar.svelte';
	const buttons = [{ icon: 'icono1' }, { icon: 'icono2' }, { icon: 'icono3' }, { icon: 'icono4' }];
	const image =
		'https://fastly.picsum.photos/id/180/200/200.jpg?hmac=YtJJ-CeQThqv_K6NzUnKS6Q8-tjxUVkSKeDsStrjEyM';
</script>

<main class="image-panel">
	<div class="left-card">
		<div class="card-image">
			<!-- svelte-ignore a11y-img-redundant-alt -->
			<img src={image} alt="Left Image" />
		</div>
		<div class="card-footer">
			<button class="btn">Subir imagen</button>
		</div>
	</div>
	<div class="right-card">
		<div class="card-image">
			<!-- svelte-ignore a11y-img-redundant-alt -->
			<img src={image} alt="Right Image" />
		</div>
		<div class="card-footer">
			<button class="btn">Girar</button>
		</div>
	</div>
</main>

<style>
	.image-panel {
		display: flex;
		flex-direction: row;
	}

	.left-card,
	.right-card {
		display: flex;
		flex-direction: column;
		flex: 1;
		padding: 10px;
		margin: 5px;
		min-height: 35vh;
	}

	.card-image {
		display: flex;
		align-items: center;
		justify-content: center;
		width: 100%;
		height: 100%;
		padding: 10px;
	}

	.card-image > img {
		max-width: 100%;
		max-height: 100%;
		object-fit: contain;
	}

	.card-footer {
		margin-top: auto;
	}

	.btn {
		padding: 10px;
		margin-top: 10px;
		color: white;
		background-color: #007bff;
		border: none;
		border-radius: 5px;
		cursor: pointer;
	}
</style>
