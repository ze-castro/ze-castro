<script lang="ts">
	import { onMount } from 'svelte';

	// media
	import logo from '$lib/assets/index/logo.webp';
	import welcomeImage from '$lib/assets/index/welcome.webp';
	import simpleWebsiteImage from '$lib/assets/index/simple-website.webp';
	import onlineStoreImage from '$lib/assets/index/online-store.webp';
	import personalizedSoftwareImage from '$lib/assets/index/personalized-software.webp';
	import clarabiaImage from '$lib/assets/clients/clarabia.webp';
	import ementifyImage from '$lib/assets/clients/menu-ementify.webp';
	import mariodukaImage from '$lib/assets/clients/marioduka.webp';
	import jotaautodetailImage from '$lib/assets/clients/jotaautodetail.webp';
	import luizaseabraImage from '$lib/assets/clients/luizaseabra.webp';
	import brandboostmediaImage from '$lib/assets/clients/brandboostmedia.webp';
	import exclusivecardetailImage from '$lib/assets/clients/exclusive-car-detail.webp';
	import jasmimdesignfloralImage from '$lib/assets/clients/jasmimdesignfloral.webp';
	import happiesImage from '$lib/assets/clients/happies.webp';

	// files
	import faqs from '$lib/assets/files/faq.json';

	// components
	import Svg from '$lib/components/svg.svelte';

	// swiper
	import Swiper from 'swiper/bundle';
	import 'swiper/css/bundle';

	// HOME
	function handleContact() {
		const email = 'ze.castro@icloud.com';
		const subject = 'Pedido de Contacto';
		const body =
			'Olá,\n\n[Escreva aqui a sua mensagem]\n\nAguardo o seu contacto.\n\nCom os melhores cumprimentos,\n[O seu nome]';
		window.location.href = `mailto:${email}?subject=${encodeURIComponent(subject)}&body=${encodeURIComponent(body)}`;
	}

	function handleButtonClick(service: string) {
		let serviceName = '';
		if (service === 'website') {
			serviceName = 'Site';
		} else if (service === 'online-store') {
			serviceName = 'Loja Online';
		} else if (service === 'personalized-software') {
			serviceName = 'Software';
		}
		const email = 'ze.castro@icloud.com';
		const subject = `Pedido de Orçamento para ${serviceName}`;
		const body = `Olá,\n\nVenho por este meio solicitar um orçamento para um(a) ${serviceName}.\n\nAguardo o seu contacto.\n\nCom os melhores cumprimentos,\n[O seu nome]`;
		window.location.href = `mailto:${email}?subject=${encodeURIComponent(subject)}&body=${encodeURIComponent(body)}`;
	}

	// Initialize Carousel
	let swiperElement: HTMLDivElement;
	onMount(() => {
		// Initialize Carousel
		const swiper = new Swiper(swiperElement, {
			// mouse control scroll
			mousewheel: {
				forceToAxis: true,
				releaseOnEdges: true
			},
			// keyboard control
			keyboard: {
				enabled: true,
				onlyInViewport: true
			},
			loop: true,
			speed: 1000,
			direction: 'horizontal',
			spaceBetween: 15,
			slidesPerView: 1,
			autoplay: {
				delay: 2000
			},
			breakpoints: {
				800: {
					slidesPerView: 5,
					spaceBetween: 50
				}
			}
		});

		// when user hovers over the carousel, stop the autoplay
		swiperElement.addEventListener('mouseenter', () => {
			swiper.autoplay.stop();
		});

		// when user leaves the carousel, start the autoplay
		swiperElement.addEventListener('mouseleave', () => {
			swiper.autoplay.start();
		});

		// for mobile, stop the autoplay when the user swipes
		swiperElement.addEventListener('touchstart', () => {
			swiper.autoplay.stop();
		});

		// for mobile, start the autoplay when the user stops swiping after 1000ms
		swiperElement.addEventListener('touchend', () => {
			setTimeout(() => {
				swiper.autoplay.start();
			}, 3000);
		});
	});

	// FAQ
	let expandedIndex: number | null = $state(null);

	function toggle(index: number) {
		expandedIndex = expandedIndex === index ? null : index;
	}
</script>

<main>
	<a id="tools-link" href="/tools">
		<p>Caixa de Ferramentas</p>
		<Svg name="arrow-right" size="0.8rem" color="var(--black)" />
	</a>
	<section id="welcome">
		<div class="logo">
			<img src={logo} alt="logo" />
			<h4>ze-castro</h4>
		</div>
		<h1>Criação de Sites Profissionais para Empresas e Pessoas</h1>
		<p>A partir de <span class="prices">399</span><span class="currency">€</span>*</p>
		<div class="links">
			<span class="btn-and-animation">
				<button id="contact-btn" onclick={handleContact}>Contacto</button>
				<span class="btn-animation"></span>
			</span>
			<a id="learn-more-link" href="#pricing">Serviços ></a>
		</div>
		<img class="welcome-image" src={welcomeImage} alt="Imagem de boas-vindas" />
	</section>
	<section id="pricing">
		<h1>Comece Agora</h1>
		<p>Preços abaixo sem IVA incluído*</p>
		<div class="pricing-cards">
			<div class="card">
				<div class="card-left">
					<h2>Site Profissional</h2>
					<ul>
						<li>
							O essencial para divulgar o seu negócio na internet, incluindo várias páginas, um
							domínio personalizado e uma conta de email profissional.
						</li>
					</ul>
					<h3>
						A partir de <span class="prices">399</span><span class="currency">€</span>
						<p>+ 29,90€ /ano</p>
					</h3>
					<button id="learn-more-btn-1" onclick={() => handleButtonClick('website')}
						>Começe Agora</button
					>
				</div>
				<div class="card-right" id="simple-website">
					<img src={simpleWebsiteImage} alt="simple-website" loading="lazy" />
				</div>
			</div>
			<div class="card">
				<div class="card-left" id="online-store">
					<img src={onlineStoreImage} alt="online-store" loading="lazy" />
				</div>
				<div class="card-right">
					<h2>Loja Online</h2>
					<ul>
						<li>
							A solução ideal para quem quer vender online, a partir do Shopify, consegue vender o
							que quiser, quando quiser e onde quiser.
						</li>
					</ul>
					<h3>
						A partir de <span class="prices">1399</span><span class="currency">€</span>
						<!-- <span class="discount">-20%</span> -->
						<p>+ 29,90€ /ano</p>
					</h3>
					<button id="learn-more-btn-2" onclick={() => handleButtonClick('online-store')}
						>Começe Agora</button
					>
				</div>
			</div>
			<div class="card">
				<div class="card-left">
					<h2>Software Personalizado</h2>
					<ul>
						<li>
							Se tem uma ideia específica para uma plataforma, entre em contato comigo para discutir
							as suas necessidades e obter um orçamento personalizado.
						</li>
					</ul>
					<h3>
						Orçamento à sua medida <p>*a partir de 999€</p>
					</h3>
					<button id="learn-more-btn-3" onclick={() => handleButtonClick('personalized-software')}
						>Peça Agora</button
					>
				</div>
				<div class="card-right" id="personalized-software">
					<img src={personalizedSoftwareImage} alt="personalized-software" loading="lazy" />
				</div>
			</div>
		</div>
	</section>
	<section id="clients">
		<h1>Com quem trabalhei?</h1>
		<p>Clientes que confiam no meu trabalho</p>
		<div class="swiper" bind:this={swiperElement}>
			<div class="swiper-wrapper">
				<div class="swiper-slide">
					<a
						href="https://clarabia.pt"
						target="_blank"
						rel="noopener noreferrer"
						aria-label="clarabia"
					></a>
					<img src={clarabiaImage} alt="website" />
				</div>
				<div class="swiper-slide">
					<a
						href="https://ementify.netlify.app"
						target="_blank"
						rel="noopener noreferrer"
						aria-label="ementify"
					></a>
					<img src={ementifyImage} alt="website" />
				</div>
				<div class="swiper-slide">
					<a
						href="https://marioduka.com/"
						target="_blank"
						rel="noopener noreferrer"
						aria-label="marioduka"
					></a>
					<img src={mariodukaImage} alt="website" />
				</div>
				<div class="swiper-slide">
					<a
						href="https://jotaautodetail.com/"
						target="_blank"
						rel="noopener noreferrer"
						aria-label="jotaautodetail"
					></a>
					<img src={jotaautodetailImage} alt="website" />
				</div>
				<div class="swiper-slide">
					<a
						href="https://luizaseabra.pt/"
						target="_blank"
						rel="noopener noreferrer"
						aria-label="luizaseabra"
					></a>
					<img src={luizaseabraImage} alt="website" />
				</div>
				<div class="swiper-slide">
					<a
						href="https://brandboostmedia-pt.onrender.com"
						target="_blank"
						rel="noopener noreferrer"
						aria-label="brandboostmedia"
					></a>
					<img src={brandboostmediaImage} alt="website" />
				</div>
				<div class="swiper-slide">
					<a
						href="https://exclusivecardetail.onrender.com"
						target="_blank"
						rel="noopener noreferrer"
						aria-label="exclusivecardetail"
					></a>
					<img src={exclusivecardetailImage} alt="website" />
				</div>
				<div class="swiper-slide">
					<a
						href="https://jasmimdesignfloral.pt/"
						target="_blank"
						rel="noopener noreferrer"
						aria-label="jasmimdesignfloral"
					></a>
					<img src={jasmimdesignfloralImage} alt="website" />
				</div>
				<div class="swiper-slide">
					<a
						href="/"
						onclick={() =>
							alert('PROJETO PRIVADO. Construção de um sistema de testes de terapia da fala.')}
						aria-label="happies"
					></a>
					<img src={happiesImage} alt="website" />
				</div>
			</div>
		</div>
	</section>
	<section id="scheduling">
		<h1>Precisa de mais informação?</h1>
		<p>Reuna comigo para discutir as suas necessidades</p>
		<div class="scheduling-container">
			<button class="scheduling-button">
				<a
					href="https://calendly.com/jose-castro-dev/esclarecimentos"
					target="_blank"
					rel="noopener noreferrer"><Svg name="phone" size="1.5rem" />Agende uma Chamada</a
				>
			</button>
			<a id="scheduling-email" href="mailto:ze.castro@icloud.com">
				em alternativa, envie-me um email<Svg name="envelope" size="1rem" color="var(--gray-4)" />
			</a>
		</div>
	</section>
	<section id="me">
		<h1>Quem sou eu?</h1>
		<p>Conheça quem cria os sites que vê aqui</p>
		<div class="me-container">
			<div class="me-image">
				<img src={logo} alt="me" />
			</div>
			<div class="me-description">
				<h2>Olá, o meu nome é José Castro</h2>
				<p>
					Engenheiro Dev-Ops de profissão e com mais de 3 anos de experiência em desenvimento de
					software para a web. O meu objetivo é ajudar empresas e pessoas a informatizarem a sua
					empresa, com sites, softwares personalizados e outros.
				</p>
				<p>
					Se procura um site ou software à medida que se destaca, entre em contato comigo para
					discutirmos as suas necessidades e obtenha um orçamento ainda hoje.
				</p>
				<a
					href="https://calendly.com/jose-castro-dev/esclarecimentos"
					target="_blank"
					rel="noopener noreferrer"
					><Svg name="phone" size="1.2rem" color="transparent" strokeColor="var(--blue)" />Agende
					uma Chamada
				</a>
			</div>
		</div>
	</section>
	<section id="faq">
		<h1>Perguntas Frequentes</h1>
		<p>Algumas das perguntas mais comuns que recebo</p>
		<div class="faq-container">
			{#each faqs as faq, i}
				<!-- svelte-ignore a11y_click_events_have_key_events -->
				<!-- svelte-ignore a11y_no_static_element_interactions -->
				<div
					class="box"
					class:expanded={expandedIndex === i}
					style:border-top={i > 0 && expandedIndex !== i - 1 ? '1px solid var(--gray-2)' : 'none'}
					onclick={() => toggle(i)}
				>
					<h2 class="box-title">{faq.question}</h2>
					<p class="box-description">{faq.answer}</p>
				</div>
			{/each}
		</div>
	</section>
	<section id="contact">
		<h1>Vamos falar?</h1>
		<p>Envie-me uma mensagem e entrarei em contato o mais breve possível</p>
		<div class="contact-box">
			<a id="contact-email" href="mailto:ze.castro@icloud.com">
				<Svg
					style="position: absolute;
                    right: 2rem;
                    bottom: 0rem;
                    transform: translate(-50%, 50%);"
					name="mouse-pointer"
					size="2.5rem"
					color="var(--black)"
				/>ze.castro@icloud.com
			</a>
		</div>
	</section>
	<section id="disclaimer">
		<p>
			*Todos os preços apresentados são meramente indicativos e podem variar consoante a
			complexidade do projeto. Para obter um orçamento, entre em contato comigo.
		</p>
		<p>
			**Os sites apresentados são projetos reais desenvolvidos por José Castro e não podem ser
			copiados ou reproduzidos sem autorização por escrito.
		</p>
		<p>
			***José Castro é um programador web registado como trabalhador independente. Caso necessite de
			fatura, esta será emitida como tal.
		</p>
		<p>
			Para mais informações sobre a política de privacidade e cookies, por favor consulte os nossos
			<a href="/terms-and-conditions">Termos & Condições</a>.
		</p>
	</section>
</main>

<style>
	#welcome,
	#clients,
	#pricing,
	#scheduling,
	#me,
	#faq,
	#contact {
		position: relative;
		z-index: 1;
		margin-bottom: 4rem;
		padding: 0 1rem;
	}

	#welcome h1,
	#clients h1,
	#pricing h1,
	#scheduling h1,
	#me h1,
	#faq h1,
	#contact h1 {
		text-align: center;
	}

	/* LOGO */
	.logo {
		height: 100%;
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
	}

	.logo img {
		width: 50px;
		height: 50px;
		border-radius: 50%;
		margin-right: 1rem;
		border: 2px solid var(--black);
	}

	.logo h4 {
		font-size: 1.3rem;
		font-weight: var(--light);
		letter-spacing: 0.01rem;
		color: var(--black);
	}

	/* TOOLS LINK */
	#tools-link {
		position: absolute;
		margin-top: 2.2rem;
		top: 0;
		right: 1rem;
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

	#tools-link:hover {
		background-color: var(--gray-2);
	}

	/* WELCOME */
	#welcome {
		width: 100%;
		min-height: auto;
		display: flex;
		flex-direction: column;
		justify-content: flex-start;
		align-items: center;
		margin-top: 2rem;
		gap: 2rem;
		overflow: hidden;
	}

	#welcome h1 {
		width: 50%;
		color: var(--black);
		font-size: var(--title);
		font-weight: var(--bold);
		text-align: center;
		z-index: 2;
	}

	#welcome p {
		width: 65%;
		color: var(--black);
		font-size: var(--subtitle);
		font-weight: var(--light);
		text-align: center;
		z-index: 2;
	}

	#welcome .links {
		width: 100%;
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
		gap: 2rem;
		z-index: 2;
	}

	#welcome .links button {
		cursor: pointer;
	}

	@keyframes animate {
		0% {
			background-position: 0%;
		}
		100% {
			background-position: 400%;
		}
	}

	#welcome button {
		width: 100px;
		height: 40px;
		color: var(--white);
		background: linear-gradient(90deg, orange, red, violet, purple, var(--blue), orange);
		background-size: 400%;
		font-size: var(--paragraph);
		font-weight: var(--regular);
		z-index: 1;
		position: relative;
		animation: animate 8s linear infinite;
	}

	#welcome button:before {
		width: 100px;
		height: 40px;
		content: '';
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		z-index: -1;
		border-radius: 40px;
		background: linear-gradient(45deg, orange, red, violet, purple, var(--blue), orange);
		background-size: 100%;
		filter: blur(7px);
		animation: animate 8s linear infinite;
	}

	#welcome a {
		font-size: var(--paragraph);
		font-weight: var(--font-weight);
		font-weight: var(--light);
		z-index: 2;
	}

	#welcome .welcome-image {
		width: 50rem;
		max-width: 98%;
		height: 25rem;
		object-fit: cover;
		border-radius: 20px;
		box-shadow: 0 0 0.5rem rgba(0, 0, 0, 0.3);
		transition: var(--slow);
	}

	/* PRICING */
	#pricing {
		width: 100%;
		min-height: auto;
		display: flex;
		flex-direction: column;
		justify-content: flex-start;
		align-items: center;
	}

	#pricing h1 {
		font-size: var(--title);
		font-weight: var(--bold);
		margin-top: 2rem;
	}

	#pricing p {
		font-size: var(--subtitle);
		font-weight: var(--light);
		margin-top: 0.7rem;
		color: var(--gray-5);
	}

	.pricing-cards {
		width: 100%;
		margin-top: 2rem;
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: flex-start;
		flex-wrap: wrap;
		gap: 2rem;
	}

	.card {
		width: 800px;
		height: 400px;
		border-radius: 1rem;
		background-color: var(--white);
		border: 1px solid rgba(224, 224, 224, 0.5);
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: stretch;
		transition: var(--slow);
	}

	.card-left,
	.card-right {
		width: 50%;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		align-items: flex-start;
		gap: 1rem;
		padding: 3rem 1.5rem;
	}

	#simple-website,
	#online-store,
	#personalized-software {
		padding: 0;
	}

	.card h2 {
		font-size: var(--faq);
		font-weight: var(--semi-bold);
		color: var(--black);
	}

	.card li {
		line-height: 2rem;
		font-size: var(--paragraph);
		font-weight: var(--light);
		color: var(--gray-4);
	}

	.card h3 {
		font-size: var(--subtitle);
		font-weight: var(--regular);
		color: var(--black);
	}

	.card h3 p {
		font-size: var(--microcopy) !important;
		color: var(--gray-4) !important;
		margin-top: 0.3rem !important;
	}

	.card button {
		width: 100%;
		height: 40px;
		font-weight: var(--light);
		font-size: var(--paragraph);
		background-color: var(--blue);
		padding: 0 1rem;
		border-radius: 0.5rem;
	}

	.card img {
		width: 100%;
		height: 100%;
		object-fit: cover;
		z-index: 1;
	}

	#simple-website img,
	#personalized-software img {
		border-top-right-radius: 1rem;
		border-bottom-right-radius: 1rem;
	}

	#online-store img {
		border-top-left-radius: 1rem;
		border-bottom-left-radius: 1rem;
	}

	#simple-website img {
		object-position: 45.5%;
	}

	/* CLIENTS */
	#clients {
		width: 100%;
		min-height: auto;
		display: flex;
		flex-direction: column;
		justify-content: flex-start;
		align-items: center;
		padding: 0;
	}

	#clients h1 {
		font-size: var(--title);
		font-weight: var(--bold);
		margin-top: 2rem;
		text-align: center;
	}

	#clients > p {
		font-size: var(--subtitle);
		font-weight: var(--light);
		margin-top: 0.7rem;
		color: var(--gray-5);
		text-align: center;
		padding: 0 1rem;
	}

	.swiper {
		width: 100%;
		display: flex;
		justify-content: center;
		align-items: center;
		padding: 2rem 5rem 5rem 5rem;
		transition: var(--slow);
	}

	.swiper-wrapper {
		width: 100%;
		display: flex;
		justify-content: flex-start;
		align-items: center;
	}

	.swiper-slide {
		height: 150px;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		gap: 2rem;
		position: relative;
		transition: var(--steady);
		user-select: none;
		border: 1px solid var(--gray-2);
		border-radius: var(--radius-2);
		background-color: var(--gray-1);
		filter: drop-shadow(0 0.5rem 0.5rem var(--shadow-1));
	}

	.swiper-slide:hover {
		transform: scale(1.03) rotate(-1deg);
		filter: drop-shadow(0 0.5rem 0.7rem var(--shadow-1));
	}

	.swiper-slide a {
		width: 100%;
		height: 100%;
		display: flex;
		justify-content: center;
		align-items: center;
		z-index: 2;
		position: absolute;
	}

	.swiper-slide a:hover {
		cursor: pointer;
	}

	.swiper-slide img {
		width: 70%;
		object-fit: cover;
	}

	/* SCHEDULING */
	#scheduling {
		width: 100%;
		min-height: auto;
		display: flex;
		flex-direction: column;
		justify-content: flex-start;
		align-items: center;
		padding-bottom: 2rem;
		background-color: var(--gray-1);
		box-shadow: inset 0 0 2rem var(--shadow-1);
	}

	#scheduling h1 {
		font-size: var(--title);
		font-weight: var(--bold);
		margin-top: 2rem;
		text-align: center;
	}

	#scheduling > p {
		font-size: var(--subtitle);
		font-weight: var(--light);
		margin-top: 0.7rem;
		color: var(--gray-5);
		text-align: center;
	}

	#scheduling .scheduling-container {
		width: 100%;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		margin-top: 3rem;
		transition: var(--slow);
	}

	#scheduling .scheduling-container button {
		width: 400px;
		height: 60px;
		font-weight: var(--light);
		color: var(--white);
		background-color: var(--blue);
		border-radius: 10rem;
		box-shadow: 0 0.2rem 1rem var(--shadow-2);
	}

	#scheduling .scheduling-container button:hover {
		transform: scale(1.05);
		box-shadow: 0 0.5rem 1.5rem var(--shadow-2);
	}

	#scheduling .scheduling-container button a {
		display: flex;
		align-items: center;
		justify-content: center;
		gap: 0.5rem;
		text-decoration: none;
		color: var(--white);
		font-size: var(--subtitle);
		font-weight: var(--semi-bold);
	}

	#scheduling .scheduling-container > a {
		display: flex;
		align-items: center;
		gap: 0.3rem;
		font-size: var(--paragraph);
		font-weight: var(--light);
		color: var(--gray-4);
		margin-top: 0.5rem;
	}

	/* ME */
	#me {
		width: 100%;
		min-height: auto;
		display: flex;
		flex-direction: column;
		justify-content: flex-start;
		align-items: center;
	}

	#me h1 {
		font-size: var(--title);
		font-weight: var(--bold);
		margin-top: 2rem;
		text-align: center;
	}

	#me > p {
		font-size: var(--subtitle);
		font-weight: var(--light);
		margin-top: 0.7rem;
		color: var(--gray-5);
		text-align: center;
	}

	.me-container {
		width: 100%;
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
		gap: 2rem;
		margin-top: 3rem;
		transition: var(--slow);
	}

	.me-image {
		width: 300px;
		height: 300px;
		border-radius: 50%;
		object-fit: cover;
		box-shadow: 0 0 1rem var(--shadow-2);
	}

	.me-image img {
		width: 100%;
		height: 100%;
		border-radius: 50%;
		object-fit: cover;
		object-position: 50% 100%;
	}

	.me-description {
		width: 50%;
		max-width: 500px;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: flex-start;
		gap: 1rem;
	}

	.me-description h2 {
		font-size: var(--faq);
		font-weight: var(--semi-bold);
		color: var(--black);
	}

	.me-description p {
		font-size: var(--paragraph);
		font-weight: var(--light);
		color: var(--gray-4);
	}

	.me-description a {
		display: flex;
		align-items: center;
		gap: 0.5rem;
		font-size: var(--paragraph);
		font-weight: var(--light);
		color: var(--blue);
	}

	/* FAQ */
	#faq {
		width: 100%;
		min-height: auto;
		display: flex;
		flex-direction: column;
		justify-content: flex-start;
		align-items: center;
	}

	#faq h1 {
		font-size: var(--title);
		font-weight: var(--bold);
		margin-top: 2rem;
		text-align: center;
	}

	#faq > p {
		font-size: var(--subtitle);
		font-weight: var(--light);
		margin-top: 0.7rem;
		color: var(--gray-5);
		text-align: center;
	}

	.faq-container {
		width: 100%;
		margin-top: 3rem;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}

	.box {
		width: 100%;
		max-width: 700px;
		overflow: hidden;
		padding: 2rem;
		cursor: pointer;
		border-top: 1px solid var(--gray-2);
		transition: var(--slow);
	}

	.box:last-of-type {
		border-bottom: 1px solid var(--gray-2);
	}

	.box-title {
		font-size: var(--faq);
		font-weight: var(--regular);
		color: var(--black);
	}

	.box-description {
		display: none;
		margin-top: 1rem;
		transition: display 0.3s ease-in-out;
		font-size: var(--paragraph);
		font-weight: var(--light);
	}

	.box.expanded .box-description {
		display: block;
	}

	.box.expanded {
		background-color: var(--gray-1);
		border: 1px solid var(--gray-2);
		border-radius: 1rem;
	}

	/* CONTACT */
	#contact {
		width: 100%;
		min-height: auto;
		display: flex;
		flex-direction: column;
		justify-content: flex-start;
		align-items: center;
	}

	#contact h1 {
		font-size: var(--title);
		font-weight: var(--bold);
		text-align: center;
	}

	#contact p {
		font-size: var(--subtitle);
		font-weight: var(--light);
		text-align: center;
		margin-top: 0.7rem;
		color: var(--gray-5);
	}

	#contact .contact-box {
		width: 100%;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		gap: 1rem;
		margin-top: 2rem;
		transition: var(--slow);
	}

	#contact .contact-box a {
		font-size: var(--email);
		font-weight: var(--light);
		color: var(--black);
		background-color: var(--gray-1);
		padding: 1rem 2rem;
		border-radius: 1rem;
		text-decoration: none;
		transition: var(--steady);
		position: relative;
		cursor: pointer;
	}

	#contact .contact-box a:hover {
		background-color: var(--gray-2);
	}

	/* DISCLAIMER */
	#disclaimer {
		width: 100%;
		min-height: auto;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		gap: 0.5rem;
		margin-top: 2rem;
		padding: 1rem;
		background-color: var(--gray-2);
	}

	#disclaimer p {
		font-size: var(--microcopy);
		font-weight: var(--light);
		color: var(--gray-5);
	}

	#disclaimer p a {
		color: var(--gray-5);
		text-decoration: underline;
	}

	/* MEDIA QUERIES */
	@media (width > 1600px) {
		.swiper-slide {
			height: 200px;
		}
	}

	@media (width < 1025px) {
		#welcome h1 {
			font-size: 3.2rem;
		}
		#pricing h1 {
			font-size: 3.2rem;
		}
		#clients h1 {
			font-size: 3.2rem;
		}
		#scheduling h1 {
			font-size: 3.2rem;
		}
		#me h1 {
			font-size: 3.2rem;
		}
		#faq h1 {
			font-size: 3.2rem;
		}
		#contact h1 {
			font-size: 3.2rem;
		}
	}

	@media (width < 800px) {
		#tools-link {
			display: none;
		}
		#welcome h1 {
			width: 95%;
			font-size: 3rem;
		}
		#welcome p {
			font-size: 1.2rem;
		}
		#welcome .links {
			flex-direction: column;
			gap: 1rem;
		}
		#welcome button {
			width: 100px;
			height: 40px;
			font-size: 1rem;
		}
		#welcome .welcome-image {
			width: 100%;
			height: 20rem;
		}
		#pricing {
			padding: 0 1rem;
		}
		#pricing h1 {
			width: 95%;
			font-size: 3rem;
		}
		#pricing p {
			font-size: 1rem;
		}
		.card {
			width: 100%;
			max-width: 600px;
			height: auto;
			justify-content: flex-start;
			align-items: center;
			padding: 1rem;
			position: relative;
			border: 1px solid var(--gray-2);
		}
		.card-left,
		.card-right {
			width: 100%;
			padding: 1.5rem 1rem;
			z-index: 2;
		}
		#simple-website,
		#online-store,
		#personalized-software {
			position: absolute;
			width: 100%;
			height: 100%;
			top: 50%;
			left: 50%;
			transform: translate(-50%, -50%);
			padding: 0;
			z-index: 1;
		}
		.card h2 {
			font-size: 1.5rem;
		}
		.card li {
			padding: 0.5rem 0 1rem 0;
			font-size: 1rem;
		}
		.card h3 {
			font-size: 1.3rem;
			font-weight: var(--semi-bold);
		}
		.card button {
			width: 100%;
			height: 40px;
			font-size: 1rem;
			border-radius: 0.5rem;
		}
		.card img {
			display: none;
		}
		#clients h1 {
			width: 95%;
			font-size: 3rem;
		}
		#clients p {
			font-size: 1rem;
		}
		.swiper {
			padding: 2rem 3rem;
		}
		.swiper-slide {
			width: 100%;
			height: 250px;
		}
		.swiper-slide img {
			width: 60%;
		}
		#scheduling h1 {
			width: 95%;
			font-size: 3rem;
		}
		#scheduling p {
			font-size: 1rem;
		}
		#scheduling .scheduling-container {
			margin-top: 2rem;
		}
		#scheduling .scheduling-container button {
			width: 300px;
			height: 50px;
		}
		#scheduling .scheduling-container button a {
			font-size: 1.2rem;
		}
		#scheduling .scheduling-container > a {
			font-size: 0.9rem;
		}
		#me h1 {
			width: 95%;
			font-size: 3rem;
		}
		#me p {
			font-size: 1rem;
		}
		.me-container {
			padding: 0 1rem;
			flex-direction: column;
			gap: 2rem;
		}
		.me-image {
			width: 200px;
			height: 200px;
		}
		.me-description {
			width: 100%;
		}
		.me-description h2 {
			font-size: 1.5rem;
			text-align: left;
		}
		.me-description p {
			font-size: 1rem;
			text-align: justify;
		}
		.me-description a {
			font-size: 1rem;
		}
		#faq h1 {
			width: 95%;
			font-size: 3rem;
		}
		#faq p {
			font-size: 1rem;
		}
		.faq-container {
			max-width: 550px;
			flex-direction: column;
		}
		.box {
			width: 100%;
			max-width: 100%;
			padding: 1rem;
		}
		.box-title {
			font-size: 1.1rem;
		}
		.box-description {
			font-size: 1rem;
		}
		#contact h1 {
			width: 95%;
			font-size: 3rem;
		}
		#contact p {
			font-size: 1rem;
		}
		#contact .contact-box {
			flex-direction: column;
			gap: 1rem;
		}
		#contact .contact-box a {
			font-size: 1.8rem;
			padding: 1rem 1.5rem;
			border-radius: 0.5rem;
		}
	}

	@media (width < 600px) {
		.swiper-slide {
			height: 150px;
		}
		.swiper-slide img {
			width: 60%;
		}
		#contact .contact-box a {
			font-size: 1.3rem;
			padding: 0.7rem 1.2rem;
			border-radius: 0.5rem;
		}
		#disclaimer p {
			font-size: 0.8rem;
		}
	}

	@media (width < 420px) {
		#welcome h1 {
			font-size: 2.5rem;
		}
		#pricing h1 {
			font-size: 2.5rem;
		}
		#clients h1 {
			font-size: 2.5rem;
		}
		#scheduling h1 {
			font-size: 2.5rem;
		}
		#me h1 {
			font-size: 2.5rem;
		}
		#faq h1 {
			font-size: 2.5rem;
		}
		#contact h1 {
			font-size: 2.5rem;
		}
	}
</style>
