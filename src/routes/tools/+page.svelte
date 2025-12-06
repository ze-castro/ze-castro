<script lang="ts">
	// components
	import Svg from '$lib/components/svg.svelte';
	import BackButton from '$lib/components/back-button.svelte';
</script>

<svelte:head>
	<title>Caixa de Ferramentas</title>
	<meta name="description" content="Uma coleção de ferramentas úteis para utilizadores da internet." />
</svelte:head>

<main class="tools">
	<BackButton link="/" />
	<h1>Caixa de Ferramentas</h1>
	<p>Uma coleção de ferramentas úteis para utilizadores da internet</p>
	<ul>
		<a href="/tools/qr-code"
			><Svg name="qr-code" size="2rem" color="var(--gray-2)" /> Gerador de QR Code
		</a>
		<a href="/tools/pdf-compressor"
			><Svg name="file" size="2rem" color="var(--gray-2)" /> Compressor de PDF
		</a>
		<a href="/tools/text-comparison"
			><Svg name="text" size="2rem" color="var(--gray-2)" /> Comparador de Textos
		</a>
		<a href="/tools/image-converter/"
			><Svg name="exchange" size="2rem" color="var(--gray-2)" /> Conversor de Imagens
		</a>
		<a href="/tools/image-compressor/">
			<Svg name="compress" size="2rem" color="var(--gray-2)" strokeColor="var(--gray-2)" /> Compressor
			de Imagens
		</a>
	</ul>
</main>

<style>
	main {
		padding: 2rem;
		display: flex;
		min-height: calc(100vh - 50px);
		flex-direction: column;
		align-items: center;
	}
	h1 {
		font-size: var(--title);
		font-weight: var(--bold);
		text-align: center;
	}
	main p {
		font-size: var(--paragraph);
		font-weight: var(--light);
		color: var(--gray-5);
		text-align: center;
		margin-bottom: 2rem;
	}
	ul {
		max-width: 800px;
		display: flex;
		flex-direction: row;
		align-items: center;
		justify-content: center;
		gap: 1.5rem;
	}
	ul a {
		width: 150px;
		height: 150px;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		gap: 1rem;
		padding: 1rem;
		background-color: var(--white);
		border-radius: 1rem;
		font-size: 1rem;
		text-align: center;
		font-weight: var(--light);
		color: var(--gray-5) !important;
		text-decoration: none !important;
		box-shadow: 0 0.5rem 1rem var(--shadow-1);
		transition: var(--steady);
	}
	ul a:hover {
		transform: translateY(-0.1rem);
		box-shadow: 0 0.8rem 1rem var(--shadow-1);
		color: var(--black) !important;
	}

	@media (max-width: 500px) {
		h1 {
			font-size: 2.2rem;
			margin-bottom: 0.5rem;
		}
		p {
			font-size: 1rem;
			margin-bottom: 1rem;
		}
		ul {
			flex-direction: column;
			gap: 1rem;
			padding: 1.5rem 0;
		}
		ul a {
			width: 100%;
			height: auto;
			flex-direction: row;
			padding: 0.7rem 1rem;
		}
	}
</style>
