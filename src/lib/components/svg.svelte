<script lang="ts">
	import { onMount } from 'svelte';

	let { name, size = '1rem', color = 'white', strokeColor = 'transparent', style = '', ...props } = $props();

	const icons = import.meta.glob('$lib/icons/*.svg', {
		query: '?raw',
		import: 'default',
		eager: true
	});

	let actualSize = $state(size);

	onMount(() => {
		if (window.innerWidth < 768) {
			actualSize = `calc(${size} * 0.7)`;
		} else {
			actualSize = size;
		}
	});

	const svg = $derived(icons[`/src/lib/icons/${name}.svg`]);

	const styledSvg = $derived(() => {
		if (!svg || typeof svg !== 'string') return '';

		return svg
			.replace(/<svg/, `<svg style="${style}" width="${actualSize}" height="${actualSize}"`)
			.replace(/fill="[^"]*"/g, `fill="${color}"`)
			.replace(/stroke="[^"]*"/g, `stroke="${strokeColor}"`)
			.replace(/<svg([^>]*?)(?!.*fill=)/, `<svg$1 fill="${color}"`)
			.replace(/<svg([^>]*?)(?!.*stroke=)/, `<svg$1 stroke="${strokeColor}"`);
	});
</script>

{@html styledSvg()}
