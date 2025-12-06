<script lang="ts">
	// libraries
	import { diffWords } from 'diff';
	import type { ChangeObject } from 'diff';

	// components
	import BackButton from '$lib/components/back-button.svelte';

	// states
	let text1 = $state('');
	let text2 = $state('');
	let result: HTMLDivElement;
	let legend: HTMLDivElement;
	let diff: ChangeObject<string>[] = $state([]);

	function compareTexts() {
		if (!text1 || !text2) {
			result.innerHTML = '<p class="error">Please enter text in both fields.</p>';
			return;
		}

		diff = diffWords(text1, text2);
		result.style.display = 'block';
		legend.style.display = 'flex';
	}

	function resetFields() {
		text1 = '';
		text2 = '';
		result.innerHTML = '';
	}
</script>

<svelte:head>
	<title>Comparador de Texto</title>
	<meta name="description" content="Compare textos e encontre diferenças rapidamente." />
</svelte:head>

<main class="tools">
	<BackButton link="/tools" />
	<h1>Comparador de Texto</h1>
	<p>Compara dois textos e mostra a diferença entre eles.</p>

	<div class="text-container">
		<textarea id="text1" placeholder="Texto 1" bind:value={text1}></textarea>
		<textarea id="text2" placeholder="Texto 2" bind:value={text2}></textarea>
		<div class="buttons">
			{#if text1 && text2}
				<button id="compare-btn" onclick={compareTexts}>Comparar</button>
			{:else}
				<button id="compare-btn" disabled>Comparar</button>
			{/if}
			<button id="reset-btn" onclick={resetFields}>Reset</button>
		</div>
	</div>

	<div id="legend" bind:this={legend}>
		<p>🟢 Texto 1</p>
		<p>🔴 Texto 2</p>
	</div>

	<div class="result" id="result" bind:this={result}>
		{#each diff as part}
			<span class:added={part.added} class:removed={part.removed}>
				{part.value}
			</span>
		{/each}
	</div>
</main>

<style>
	.text-container {
		width: 100%;
		display: flex;
		flex-wrap: wrap;
		align-items: center;
		justify-content: center;
		gap: 2rem;
	}

	.text-container textarea {
		width: 45%;
		min-height: 200px;
		resize: none;
		padding: 1rem;
		font-size: var(--microcopy);
	}

	.text-container .buttons {
		display: flex;
		gap: 1rem;
	}

	#compare-btn {
		background-color: var(--light-blue);
	}

	#legend {
		padding: 3rem 0 1rem 0;
		display: none;
		align-items: center;
		gap: 1.5rem;
	}

	#legend p {
		color: var(--gray-4);
	}

	#result {
		width: 100%;
		max-width: 600px;
		display: none;
		padding: 1rem;
		border: 1px solid var(--gray-2);
		border-radius: var(--radius-4);
		margin-top: -2rem;
	}

	.added {
		color: var(--red);
		text-decoration: line-through;
		background-color: #ffdddd;
	}

	.removed {
		color: var(--green);
		background-color: #ddffdd;
	}

	@media (max-width: 768px) {
		.text-container {
			flex-direction: column;
			gap: 1rem;
		}

		.text-container textarea {
			width: 100%;
		}

		#result {
			margin-top: -1rem;
		}
	}
</style>
