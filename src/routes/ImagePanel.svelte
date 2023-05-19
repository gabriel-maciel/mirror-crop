<script lang="ts">
	import ButtonBar from './ButtonBar.svelte';
	import { onMount } from 'svelte';

	const buttons = [{ icon: 'icono1' }, { icon: 'icono2' }, { icon: 'icono3' }, { icon: 'icono4' }];
	const image =
		'https://fastly.picsum.photos/id/180/200/200.jpg?hmac=YtJJ-CeQThqv_K6NzUnKS6Q8-tjxUVkSKeDsStrjEyM';
	let leftImageElement: HTMLImageElement;
	let imgElement: HTMLImageElement;
	let currentRotation = 0;
	let canvas: HTMLCanvasElement;
	let ctx: CanvasRenderingContext2D | null;

	function clickUpload() {
		let uploadElement = document.getElementById('upload');
		if (uploadElement) {
			uploadElement.click();
		}
	}

	async function uploadImage(event: Event) {
		const target = event.target as HTMLInputElement;
		const file = target.files?.[0];

		if (file) {
			const imageDataUrl = URL.createObjectURL(file);

			let img = new Image();
			img.crossOrigin = 'Anonymous';
			img.onload = () => {
				imgElement = img; // Update imgElement with the new image
				drawRotated.call(img);
				URL.revokeObjectURL(imageDataUrl);
			};
			img.src = imageDataUrl;

			leftImageElement.src = imageDataUrl; // set the src of leftImageElement to the new image
		}
	}

	onMount(() => {
		if (!canvas) throw new Error('Canvas no está definido');

		ctx = canvas.getContext('2d');
		if (!ctx) throw new Error('Contexto de canvas no está definido');

		imgElement = new Image();
		imgElement.crossOrigin = 'Anonymous';
		imgElement.onload = drawRotated.bind(imgElement);
		imgElement.src = image;
	});

	function drawRotated(this: HTMLImageElement) {
		if (!ctx || !canvas) throw new Error('Contexto de canvas no está definido');

		ctx.clearRect(0, 0, canvas.width, canvas.height);
		ctx.save();
		ctx.translate(canvas.width / 2, canvas.height / 2);
		ctx.rotate((currentRotation * Math.PI) / 180);
		ctx.drawImage(this, -this.width / 2, -this.height / 2);
		ctx.restore();
	}

	function rotate() {
		currentRotation += 90;
		if (canvas && ctx && imgElement) {
			drawRotated.call(imgElement);
		}
	}

	function download() {
		if (!canvas) throw new Error('Canvas no está definido');

		let link = document.createElement('a');
		link.download = 'download.png';
		link.href = canvas.toDataURL();
		link.click();
	}
</script>

<main class="image-panel">
	<div class="left-card">
		<div class="card-image">
			<!-- svelte-ignore a11y-img-redundant-alt -->
			<img bind:this={leftImageElement} src={image} alt="Left Image" />
		</div>
		<div class="card-footer">
			<input type="file" id="upload" accept="image/*" on:change={uploadImage} hidden />
			<button class="btn" on:click={clickUpload}>Upload image</button>
		</div>
	</div>
	<div class="right-card">
		<div class="card-image">
			<!-- svelte-ignore a11y-img-redundant-alt -->
			<canvas bind:this={canvas} width="200" height="200" class="canvas-image" />
		</div>
		<div class="card-footer">
			<button class="btn" on:click={rotate}>Rotate</button>
			<button class="btn" on:click={download}>Download</button>
		</div>
	</div>
</main>

<style>
	.image-panel {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
	}

	.left-card,
	.right-card {
		display: flex;
		flex-direction: column;
		flex: 1;
		padding: 10px;
		margin: 5px;
		min-height: 35vh;
		box-shadow: 0 0 1rem rgba(0, 0, 0, 0.1);
		border-radius: 1rem;
	}

	.card-image {
		display: flex;
		align-items: center;
		justify-content: center;
		width: 100%;
		height: 100%;
		padding: 10px;
	}

	.card-image > img,
	.canvas-image {
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
