<script lang="ts">
	// libraries
	import compress from 'browser-image-compression';
	import JSZip from 'jszip';

	// components
	import BackButton from '$lib/components/back-button.svelte';

	// variables
	let qualityValue: number = $state(50);
	let images: File[] = $state([]);
	const compressedImages: File[] = [];
	let logMessage: string = $state('');
	let isCompressing: boolean = $state(false);
	let isCompressed: boolean = $state(false);

	function removeImage(imageToRemove: File) {
		images = images.filter((image) => image !== imageToRemove);
		logMessage = `Imagem ${imageToRemove.name} removida.`;
	}

	async function compressImages(files: File[], quality: number) {
		isCompressing = true;
		logMessage = `Comprimindo...`;

		try {
			await Promise.all(
				files.map(async (file) => {
					const compressedImage = await compress(file, {
						maxSizeMB: quality / 100,
						alwaysKeepResolution: true
					});
					compressedImages.push(compressedImage);
				})
			);
		} catch (error) {
			logMessage = `Erro ao comprimir a imagem.`;
			isCompressing = false;
			return;
		}

		isCompressing = false;
		isCompressed = true;
		logMessage = `Tudo comprimido com sucesso.`;
	}

	async function downloadImages() {
		logMessage = `Fazendo download das imagens...`;
		const link = document.createElement('a');
		if (compressedImages.length === 1) {
			const blob = compressedImages[0];
			link.href = URL.createObjectURL(blob);
			link.download = `compressed_1.${blob.type.split('/')[1]}`;
		} else {
			logMessage = `Criando ficheiro .zip...`;
			const zip = new JSZip();
			compressedImages.forEach((blob, index) => {
				zip.file(`compressed_${index + 1}.${blob.type.split('/')[1]}`, blob);
			});
			const content = await zip.generateAsync({ type: 'blob' });
			link.href = URL.createObjectURL(content);
			link.download = 'compressed_images.zip';
		}
		document.body.appendChild(link);
		link.click();
		document.body.removeChild(link);
		logMessage = `Download completo.`;
	}
</script>

<main class="tools">
	<BackButton link="/tools" />
	<h1>Compressor de Imagens</h1>
	<p>Comprime imagens PNG, JPEG, WEBP</p>
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
				<button onclick={() => !isCompressing && removeImage(image)}>
					<img src={URL.createObjectURL(image)} alt="Preview da Imagem {image.name}" />
				</button>
			{/each}
		</div>
	{/if}

	<div class="settings">
		<div class="setting">
			<label for="quality">Qualidade</label>
			<input type="range" id="quality" min="1" max="100" bind:value={qualityValue} />
			<span id="qualityValue">{qualityValue}%</span>
		</div>
	</div>

	{#if images.length > 0}
		<button
			id="compressBtn"
			disabled={isCompressing}
			onclick={() => compressImages(images, qualityValue)}>Comprimir</button
		>
		<p class="log">{logMessage}</p>
	{:else}
		<button id="compressBtn" disabled>Comprimir</button>
	{/if}

	{#if !isCompressing && isCompressed}
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
	.setting {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		gap: 1rem;
	}
	.setting span {
		font-size: var(--microcopy);
		font-weight: var(--light);
		margin-top: -0.5rem;
	}
	.setting label {
		font-weight: var(--light);
		color: var(--gray-4);
	}
	.log {
		margin-top: 1rem;
	}
	.download-btn {
		margin-top: 1rem;
	}
</style>
