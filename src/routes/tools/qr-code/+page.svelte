<script lang="ts">
	// libraries
	import QRCode from 'qrcode';

	// components
	import BackButton from '$lib/components/back-button.svelte';

	// variables
	let qrCodeDataUrl: string | null = $state(null);
	let linkInput: string = $state('');
	let canvas: HTMLCanvasElement;
	let downloadBtn: HTMLButtonElement;

	function generateQR() {
		const link = linkInput.trim();
		if (!link) {
			alert('Introduza um link ou texto para gerar o código QR.');
			return;
		}

		canvas.innerHTML = '';

		QRCode.toCanvas(canvas, link, { margin: 1, width: 200 }, (error: Error | null | undefined) => {
			if (error) {
				console.error('Erro ao gerar o código QR:', error);
				alert('Ocorreu um erro ao gerar o código QR. Tente novamente.');
				return;
			}

			canvas.style.display = 'block';
			qrCodeDataUrl = canvas.toDataURL('image/png');
			downloadBtn.style.display = 'block';
		});
	}

	function downloadQR() {
		if (!qrCodeDataUrl) return;

		const link = document.createElement('a');
		link.href = qrCodeDataUrl;
		link.download = 'qrcode.png';
		document.body.appendChild(link);
		link.click();
		document.body.removeChild(link);
	}
</script>

<svelte:head>
	<title>Gerador de Códigos QR</title>
	<meta
		name="description"
		content="Gere códigos QR rapidamente a partir de qualquer texto ou link."
	/>
</svelte:head>

<main class="tools">
	<BackButton link="/tools" />
	<h1>Gerador de Códigos QR</h1>
	<p>Insira o texto ou link que deseja converter em um código QR</p>
	<input
		type="text"
		id="linkInput"
		bind:value={linkInput}
		placeholder="Introduza o texto ou link aqui (ex: Teste)"
	/>
	{#if linkInput}
		<button onclick={generateQR}>Começar</button>
	{:else}
		<button disabled>Começar</button>
	{/if}
	<div id="qrCanvas">
		<canvas bind:this={canvas}></canvas>
	</div>
	<button id="downloadBtn" style="display: none" bind:this={downloadBtn} onclick={downloadQR}>
		Download QR Code
	</button>
</main>

<style>
	/* QR CODE */
	#qrCanvas {
		width: 200px;
		height: 200px;
		margin: 2rem 0 1rem 0;
	}

	#qrCanvas canvas {
		display: none;
		width: 100%;
		height: 100%;
		box-shadow: 1rem 1rem 2rem var(--shadow-2);
	}
</style>
