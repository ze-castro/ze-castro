<script lang="ts">
	import { page } from '$app/state';
</script>

<main>
	<h1>
		A página <span>{page.url.pathname}</span> não existe.
	</h1>
	<p>Por favor, verifique o URL e tente novamente.</p>
	<div class="links">
		<a href="/">Voltar ao Início</a>
		<a href="/tools">Caixa de Ferramentas</a>
	</div>
</main>

<style>
	main {
		padding: 2rem;
		display: flex;
		min-height: calc(100vh - 50px);
		flex-direction: column;
		align-items: center;
        justify-content: center;
	}
	main h1 {
		font-size: var(--title);
		font-weight: var(--bold);
		text-align: center;
	}
	main h1 span {
        word-break: break-word;
		background-color: var(--gray-2);
		padding: 0.5rem 1rem;
		border-radius: var(--radius-3);
	}
	main p {
		font-size: var(--paragraph);
		font-weight: var(--light);
		color: var(--gray-5);
		text-align: center;
		margin-top: 1rem;
	}
    .links {
        margin-top: 2rem;
        display: flex;
        align-items: center;
        gap: 3rem;
    }
    .links a {
        font-size: var(--subtitle);
        font-weight: var(--light);
        color: var(--blue);
    }

    @media (width <= 768px) {
        .links {
            flex-direction: column;
            gap: 1.5rem;
        }
    }
</style>
