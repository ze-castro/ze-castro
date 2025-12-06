<script lang="ts">
	// media
	import favicon from '$lib/assets/favicon.ico';
	import appleTouchIcon from '$lib/assets/index/logo.webp';

	// components
	import Cookies from '$lib/components/cookies.svelte';
	import Footer from '$lib/components/footer.svelte';

	// styles
	import '$lib/styles/defaults.css';

	let { children } = $props();
	export const prerender = true;
</script>

<svelte:head>
	<meta charset="utf-8" />
	<meta http-equiv="x-ua-compatible" content="IE=edge" />
	<meta name="viewport" content="width=device-width, initial-scale=1.0" />
	<!-- keywords -->
	<meta
		name="keywords"
		content="criação de sites, desenvolvimento web, design de sites, agência de web design, desenvolvimento de sites, e-commerce, plataforma de e-commerce, presença online, marketing digital, soluções web, website profissional, website personalizado, website responsivo, otimização para motores de busca, SEO, marketing de conteúdo, análise web, hospedagem de sites, domínio, certificado SSL, manutenção de sites, suporte técnico, criação de sites em Braga, desenvolvimento web em Portugal, agência de web design em Braga, sites para empresas em Braga, sites para empresas em Portugal, sites para negócios locais, sites para pequenas empresas, sites para startups, sites para profissionais, criação de sites para imobiliárias, criação de sites para construtoras, criação de sites para restaurantes, criação de sites para hotéis, criação de sites para advogados, criação de sites para médicos, website de alta performance, website seguro, website acessível, website otimizado para mobile, website personalizado para o seu negócio, website que vende, website que gera leads, website que aumenta a sua visibilidade online, website que melhora a sua reputação online, website que te ajuda a crescer o seu negócio, preciso de um site profissional, como ter um site para a minha empresa, qual a melhor plataforma para criar um site, quanto custa criar um site, agências de web design em Braga, desenvolvimento de sites personalizados, soluções de e-commerce para pequenas empresas, aumentar as vendas online, melhorar a experiência do cliente online, sites braga, fazer sites braga, sites portugal, site online portugal, sites online braga, construção de sites, preciso de um site, site para a minha empresa, sites de imobiliário, sites para o meu negócio"
	/>
	<!-- title and description -->
	<title>Sites para Empresas e Pessoas</title>
	<meta
		name="description"
		content="Sites adaptados às suas necessidades específicas, priorizando a privacidade e otimizando para o melhor desempenho."
	/>
	<!-- sharing tags -->
	<meta property="og:title" content="Zé Castro" />
	<meta property="og:description" content="Sites para Empresas e Pessoas" />
	<meta property="og:image" content="https://ze-castro.onrender.com/index/logo.webp" />
	<meta property="og:url" content="https://ze-castro.onrender.com/" />
	<meta property="og:type" content="website" />
	<!-- Apple Icon when save to phone -->
	<link rel="apple-touch-icon" href={appleTouchIcon} />
	<!-- favicon -->
	<link rel="icon" href={favicon} />
</svelte:head>

<Cookies />

{@render children()}

<Footer />
