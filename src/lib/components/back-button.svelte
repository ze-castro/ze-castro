<script lang="ts">
	// components
	import Svg from './svg.svelte';

	// props
	let { link } = $props();
</script>

<a id="back" href={link}><Svg name="arrow-left" size="0.9rem" color="var(--black)" /> Voltar </a>

<style>
	/* BACK BUTTON */
	#back {
		position: absolute;
		top: 1rem;
		left: 1rem;
		padding: 0.7rem 1rem;
		display: flex;
		justify-content: center;
		align-items: center;
		gap: 0.7rem;
		font-weight: var(--light);
		background-color: var(--gray-1);
		color: var(--gray-5);
		border-radius: 1rem;
		z-index: 2;
		text-decoration: none;
		transition: var(--steady);
	}

	#back:hover {
		background-color: var(--gray-2);
	}

	@media (max-width: 500px) {
		#back {
			display: none;
		}
	}
</style>
