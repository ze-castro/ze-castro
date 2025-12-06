<script lang="ts">
    // media
    import logo from '$lib/assets/index/logo.webp';
</script>

<nav>
	<img src={logo} alt="Logo" />
	<h3><a href="/">José Castro</a></h3>
</nav>
<section>
	<h1>Termos & Condições</h1>

	<p>
		Ao aceder a este website, concorda com os Termos & Condições de utilização do mesmo. Se não
		concordar com os Termos & Condições, por favor, não aceda a este website.
	</p>

	<h2>1. Informação Legal</h2>

	<p>Este website é propriedade de José Castro, com sede em Braga, Portugal.</p>

	<h2>2. Propriedade Intelectual</h2>

	<p>
		Todo o conteúdo presente neste website é propriedade intelectual de José Castro. Qualquer
		utilização do conteúdo presente neste website sem autorização prévia é estritamente proibida.
	</p>

	<h2>3. Proteção de Dados</h2>

	<p>
		Este site cumpre o Regulamento Geral sobre a Proteção de Dados (RGPD) da UE. Recolhe e trata
		dados pessoais apenas conforme necessário para fornecer os serviços esperados.
	</p>

	<h2>4. Cookies</h2>

	<p>
		Este website utiliza cookies para melhorar a experiência do utilizador. Ao utilizar este site,
		concorda com a utilização de cookies.
	</p>

	<h2>5. Limitação de Responsabilidade</h2>

	<p>
		José Castro não se responsabiliza por quaisquer danos diretos, indiretos, incidentais ou
		consequenciais resultantes da utilização ou incapacidade de utilização deste website.
	</p>

	<h2>6. Ligações Externas</h2>

	<p>
		Este site pode conter ligações para outros websites externos. José Castro não é responsável pelo
		conteúdo ou práticas de privacidade dos mesmos.
	</p>

	<h2>7. Direitos do Consumidor</h2>

	<p>
		Os serviços oferecidos neste site estão sujeitos às leis de proteção do consumidor portuguesas e
		da UE. Informações sobre devoluções e reembolsos podem ser encontradas na secção abaixo.
	</p>

	<h2>8. Mensalidade</h2>

	<p>
		Ao adquirir um dos nossos serviços, concorda em pagar a mensalidade correspondente ao mesmo. A
		mensalidade começa no início do segundo mês e não é reembolsável. A mesma tem o propósito de
		cobrir os custos de alojamento e atualizações de segurança do website.
	</p>

	<h2>9. Devoluções e Reembolsos</h2>

	<p>
		Visto a categoria de serviços oferecidos neste website, não são aceites devoluções ou
		reembolsos. Se tiver alguma questão ou problema com os serviços prestados, por favor,
		contacte-me através de
		<a href="mailto:ze.castro@icloud.com">ze.castro@icloud.com</a>.
	</p>

	<h2>10. Alterações aos Termos & Condições</h2>

	<p>
		José Castro reserva-se ao direito de alterar os Termos & Condições de utilização deste website
		sem aviso prévio. Ao continuar a utilizar este website, concorda com os Termos & Condições
		atualizados.
	</p>

	<h2>11. Contacto</h2>

	<p>
		Para qualquer questão relacionada com os Termos & Condições de utilização deste website, por
		favor, contacte-nos através do email
		<a href="mailto:ze.castro@icloud.com">ze.castro@icloud.com</a>.
	</p>

	<p>Última atualização: 3 de julho de 2024</p>
</section>

<style>
	nav {
		display: flex;
		align-items: center;
		padding: 0 10rem;
		gap: 1rem;
		height: 60px;
		background-color: var(--white);
		box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
	}

	nav img {
		width: 40px;
		height: 40px;
		border-radius: 50%;
	}

	nav h3 {
		font-size: var(--subtitle);
		font-weight: var(--light);
		color: var(--black);
	}

	nav h3 a {
		text-decoration: none !important;
		color: var(--black) !important;
	}

	section {
		width: 100%;
		display: flex;
		flex-direction: column;
		gap: 1rem;
		padding: 2rem 10rem;
	}

	section h1 {
		font-size: var(--title);
		font-weight: var(--bold);
		color: var(--black);
	}

	section h2 {
		font-size: var(--subtitle);
		font-weight: var(--semi-bold);
		color: var(--black);
		margin-top: 1rem;
	}

	section p {
		font-size: var(--paragraph);
		font-weight: var(--light);
		color: var(--black);
		text-align: justify;
	}

	/* MEDIA QUERIES */
	@media (width < 1000px) {
		nav {
			padding: 0 5rem;
		}

		section {
			padding: 2rem 5rem;
		}

		section h1 {
			font-size: 3rem;
		}
	}

	@media (width < 800px) {
		nav {
			padding: 0 2rem;
		}

		section {
			padding: 2rem 2rem;
		}

		section h1 {
			font-size: 2rem;
		}

		section h2 {
			font-size: 1.2rem;
		}

		section p {
			font-size: 1rem;
		}
	}

	@media (width < 600px) {
		nav {
			padding: 0 1rem;
		}

		section {
			padding: 1rem;
		}

		section h1 {
			font-size: 1.5rem;
		}

		section h2 {
			font-size: 1rem;
		}

		section p {
			font-size: 0.9rem;
		}
	}
</style>
