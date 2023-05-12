<script lang="ts">
	let githubIcon = "https://raw.githubusercontent.com/FortAwesome/Font-Awesome/master/svgs/brands/github.svg";
	let twitterIcon = "https://raw.githubusercontent.com/FortAwesome/Font-Awesome/master/svgs/brands/twitter.svg";
  
	const openInNewTab = (url: string) => {
	  window.open(url, '_blank');
	};
</script>

<header class="header">
	<div class="tittle">
		<h1 class="font-mono tracking-tight text-xl">MirrorCrop</h1>
		<br />
		<h2 class="font-mono font-bold text-gray-600">Flip or rotate your image</h2>
	</div>
	<div class="social">
		<button class="social-button" on:click={() => openInNewTab('https://github.com/gabriel-maciel/mirror-crop')}>
		  <img class="social-button-icon" src={githubIcon} alt="GitHub logo" /> Star on Github
		</button>
		<button class="social-button" on:click={() => openInNewTab('https://twitter.com')}>
		  <img class="social-button-icon" src={twitterIcon} alt="Twitter logo" />
		</button>
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

	.social {
		display: flex;
		justify-content: space-evenly;
		align-items: flex-end;
	}

	.social-button-icon {
		width: 1rem;
	}

	.social-button {
    display: flex;
    align-items: center;
    gap: 0.5rem; /* Espacio entre el ícono y el texto */
    padding: 0.5rem;
    background-color: #007bFF;
    color: white;
    border: none;
    border-radius: 0.5rem;
    cursor: pointer;
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
