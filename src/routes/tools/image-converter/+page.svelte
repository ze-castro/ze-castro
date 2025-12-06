<script lang="ts">
	// libraries
	import JSZip from 'jszip';

	// components
	import BackButton from '$lib/components/back-button.svelte';

	// variables
	let images: File[] = $state([]);
	const convertedImages: File[] = [];
	let logMessage: string = $state('');
	let isConverting: boolean = $state(false);
	let isConverted: boolean = $state(false);
	let formatOut: string = $state('');

	function removeImage(imageToRemove: File) {
		images = images.filter((image) => image !== imageToRemove);
		logMessage = `Imagem ${imageToRemove.name} removida.`;
	}

	async function convertImages(files: File[], format: string) {
		isConverting = true;
		logMessage = `Convertendo...`;

		try {
			await Promise.all(
				files.map(async (file) => {
					const img = new Image();
					const url = URL.createObjectURL(file);

					await new Promise((resolve, reject) => {
						img.onload = resolve;
						img.onerror = reject;
						img.src = url;
					});

					const canvas = document.createElement('canvas');
					canvas.width = img.naturalWidth;
					canvas.height = img.naturalHeight;

					const ctx = canvas.getContext('2d', { alpha: true });
					if (!ctx) {
						throw new Error('Não foi possível obter o contexto de renderização 2D');
					}
					ctx.drawImage(img, 0, 0);

					const mimeType = `image/${format}`;
					const blob: Blob | null = await new Promise((resolve) =>
						canvas.toBlob(resolve, mimeType, 1.0)
					);

					URL.revokeObjectURL(url);

					if (blob) {
						convertedImages.push(new File([blob], file.name, { type: blob.type }));
					}
				})
			);
		} catch (error) {
			logMessage = `Erro ao converter a imagem.`;
			isConverting = false;
			return;
		}

		isConverting = false;
		isConverted = true;
		logMessage = `Tudo convertido com sucesso.`;
	}

	async function downloadImages() {
		logMessage = `Fazendo download das imagens...`;
		const link = document.createElement('a');
		if (convertedImages.length === 1) {
			const blob = convertedImages[0];
			link.href = URL.createObjectURL(blob);
			link.download = `converted_1.${blob.type.split('/')[1]}`;
		} else {
			logMessage = `Criando ficheiro .zip...`;
			const zip = new JSZip();
			convertedImages.forEach((blob, index) => {
				zip.file(`converted_${index + 1}.${blob.type.split('/')[1]}`, blob);
			});
			const content = await zip.generateAsync({ type: 'blob' });
			link.href = URL.createObjectURL(content);
			link.download = 'converted_images.zip';
		}
		document.body.appendChild(link);
		link.click();
		document.body.removeChild(link);
		logMessage = `Download completo.`;
	}
</script>

<main class="tools">
	<BackButton link="/tools" />
	<h1>Conversor de Imagens</h1>
	<p>Converte imagens PNG, JPEG, WEBP</p>
	<label for="fileInput" class="file-input-label">
		<span>Clique para adicionar imagens</span>
	</label>

	<input
		type="file"
		id="fileInput"
		class="file-input"
		accept="image/png, image/jpeg, image/jpg, image/webp"
		multiple
		onchange={(e) => {
			images = Array.from((e.target as HTMLInputElement).files || []);
		}}
	/>

	{#if images.length > 0}
		<div id="image-container">
			{#each images as image}
				<button onclick={() => !isConverting && removeImage(image)}>
					<img src={URL.createObjectURL(image)} alt="Preview da Imagem {image.name}" />
				</button>
			{/each}
		</div>
	{/if}

	<div class="settings">
		<label for="format">Formato de Saída:</label>
		<select id="output" bind:value={formatOut}>
			<option value="" disabled selected>Selecione o formato</option>
			<option value="jpeg">JPEG</option>
			<option value="png">PNG</option>
			<option value="webp">WEBP</option>
		</select>
	</div>

	{#if images.length > 0 && formatOut}
		<button id="convertBtn" disabled={isConverting} onclick={() => convertImages(images, formatOut)}
			>Converter</button
		>
		<p class="log">{logMessage}</p>
	{:else}
		<button id="convertBtn" disabled>Converter</button>
	{/if}

	{#if !isConverting && isConverted}
		<button id="downloadBtn" class="download-btn" onclick={downloadImages}>Download</button>
	{/if}
</main>

<style>
	#image-container {
		width: 100%;
		max-width: 700px;
		overflow-x: auto;
		background-color: var(--gray-1);
		border-radius: var(--radius-4);
		display: flex;
		align-items: center;
		gap: 1rem;
		padding: 1rem;
		margin: 1rem 0;
	}
	#image-container button {
		border: none;
		background: none;
		cursor: pointer;
		padding: 0;
		margin: 0;
		border-radius: var(--radius-4);
	}
	#image-container img {
		width: 100%;
		max-height: 100px;
		border-radius: var(--radius-4);
		box-shadow: 0 0.5rem 1rem var(--shadow-2);
	}
	.file-input-label {
		display: inline-block;
		padding: 2rem 2rem;
		background-color: var(--gray-1);
		border: 0.1rem dashed var(--gray-2);
		color: var(--gray-4);
		border-radius: var(--radius-4);
		font-weight: var(--light);
		cursor: pointer;
		transition: var(--steady);
	}
	.file-input {
		display: none;
	}
	.settings {
		display: flex;
		align-items: center;
		justify-content: center;
		border: 1px solid var(--gray-2);
		border-radius: var(--radius-4);
		padding: 2rem;
		margin: 1rem 0;
	}
	.settings select {
		margin-left: 1rem;
		padding: 0.5rem 1rem;
		border-radius: var(--radius-4);
		border: 1px solid var(--gray-2);
		background-color: var(--gray-1);
		color: var(--gray-4);
	}
	.log {
		margin-top: 1rem;
	}
	.download-btn {
		margin-top: 1rem;
	}
</style>
