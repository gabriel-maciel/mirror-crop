<script lang="ts">
	import { onMount } from 'svelte';

	let currentRotation = 0;
	let canvas: HTMLCanvasElement;
	let ctx: CanvasRenderingContext2D | null;
	let isImageLoaded = false;
	let uploadedImage: HTMLImageElement | null = null;

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
			const uploadIcon = document.getElementById('uploadIcon');
			uploadedImage = document.getElementById('uploadedImage') as HTMLImageElement;

			if (uploadedImage) {
				uploadedImage.src = imageDataUrl;
				uploadedImage.style.display = 'block';
			}

			if (uploadIcon) {
				uploadIcon.style.display = 'none';
			}

			let img = new Image();
			img.crossOrigin = 'Anonymous';
			img.onload = () => {
				drawRotated.call(img);
				URL.revokeObjectURL(imageDataUrl);
				isImageLoaded = true;
			};
			img.src = imageDataUrl;
		}
	}

	onMount(() => {
		if (!canvas) throw new Error('Canvas no está definido');
		ctx = canvas.getContext('2d');
		if (!ctx) throw new Error('Contexto de canvas no está definido');
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
		if (canvas && ctx && isImageLoaded && uploadedImage) {
			currentRotation += 90;
			drawRotated.call(uploadedImage);
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
			<!-- svelte-ignore a11y-click-events-have-key-events -->
			<img
				class="upload-icon"
				id="uploadIcon"
				src="/upload-icon.svg"
				alt="Upload icon"
				on:click={clickUpload}
			/>
			<!-- svelte-ignore a11y-img-redundant-alt -->
			<img alt="An image" id="uploadedImage" style="display: none;" />
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
			<button class="btn" on:click={rotate} disabled={!isImageLoaded}>Rotate</button>
			<button class="btn" on:click={download} disabled={!isImageLoaded}>Download</button>
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

	.upload-icon {
		width: 7rem;
		height: 7rem;
		opacity: 0.4;
	}

	.upload-icon:hover {
		cursor: pointer;
	}
</style>
