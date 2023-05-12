<script>
	import logo from '$lib/images/svelte-logo.svg';
	import github from '$lib/images/github.svg';
</script>

<header class="header">
	<div class="tittle">
		<h1 class="font-mono tracking-tight text-xl">MirrorCrop</h1>
		<br />
		<h2 class="font-mono font-bold text-gray-600">Flip or rotate your image</h2>
	</div>
	<div class="social">
		<a>Star on Github</a>
		<a>Twitter</a>
	</div>
</header>

<style>
	.header {
		display: flex;
		flex-direction: row;
	}

	.tittle,
	.social {
		flex: 1;
		padding: 10px;
		margin: 5px;
	}

	.font-mono {
		font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, Liberation Mono, Courier New,
			monospace;
	}

	.tracking-tight {
		letter-spacing: -0.025em;
	}

	.text-xl {
		font-size: 1.25rem;
		line-height: 1.75rem;
	}

	.font-bold {
		font-weight: 700;
	}

	.text-gray-600 {
		--tw-text-opacity: 1;
		color: rgb(75 85 99 / var(--tw-text-opacity));
	}
</style>
