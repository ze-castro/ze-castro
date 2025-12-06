<script lang="ts">
    const currentYear: number = new Date().getFullYear();
</script>

<footer>
	<p>©<span id="year">{currentYear}</span> José Castro</p>
</footer>

<style>
	/* FOOTER */
	footer {
		width: 100%;
		height: 50px;
		background-color: var(--black);
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
		gap: 0.4rem;
	}

	footer p {
		font-size: 1.1rem;
		font-weight: var(--light);
		text-align: center;
		color: var(--white);
	}
	@media (width < 800px) {
		footer p {
			font-size: 1rem;
		}
	}

	@media (width < 600px) {
		footer p {
			font-size: 0.7rem;
		}
	}
</style>
