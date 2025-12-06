<script lang="ts">
	import { onMount } from 'svelte';

	let cookieBanner: HTMLDivElement;

    // on load of the page
	onMount(() => {
		const cookies = localStorage.getItem('cookies');

		// check cookies
		if (verifyCookies()) {
			// hide the cookies div
			cookieBanner.style.display = 'none';
		} else {
			// show cookies div
			setTimeout(() => {
				cookieBanner.style.bottom = '2rem';
			}, 1000);
		}

		// detail the cookies we use in the website
		console.log('%cCookies we use:', 'font-weight: bold; font-size: 1.2rem;');
		console.log('\n');
		console.log('%cGoogle Analytics', 'font-weight: bold; font-size: 1.2rem;');
		console.log('https://policies.google.com/privacy');
		console.log('We use Google Analytics to track the number of visitors of our website.');
		console.log('\n');
		console.log('%cLocal Storage', 'font-weight: bold; font-size: 1.2rem;');
		console.log(
			'We use local storage to store if the user has accepted the cookies previously, that way we do not show the cookies bar every time the user visits the website.'
		);
		console.log('\n');
		console.log('We do not store any user data. Thank you for visiting our website!');
	});

	function acceptCookies() {
		loadGoogleAnalytics();
		localStorage.setItem('cookies', 'accepted');
		cookieBanner.style.bottom = '-5rem';
		setTimeout(() => {
			cookieBanner.style.display = 'none';
		}, 500);
	}

	function verifyCookies() {
		const cookies = localStorage.getItem('cookies');
		if (cookies === 'accepted') {
			loadGoogleAnalytics();
			return true;
		}
		return false;
	}

	// load Google Analytics
	function loadGoogleAnalytics() {
		const script = document.createElement('script');
		script.src = 'https://www.googletagmanager.com/gtag/js?id=G-ZQJTJZDSM8';
		script.async = true;
		document.head.appendChild(script);

		(window as any).dataLayer = (window as any).dataLayer || [];
		function gtag(...args: any[]) {
			(window as any).dataLayer.push(args);
		}
		gtag('js', new Date());
		gtag('config', 'G-ZQJTJZDSM8');
	}
</script>

<div id="cookies" bind:this={cookieBanner}>
	<p>Este site utiliza cookies para garantir que tenha a melhor experiência nesta sessão.</p>
	<button onclick={() => acceptCookies()}>Entendi</button>
</div>

<style>
	/* COOKIES */
	#cookies {
		width: auto;
		height: 80px;
		padding: 0 2rem;
		background-color: var(--white);
		border-radius: 0.5rem;
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
		gap: 2rem;
		position: fixed;
		bottom: -6rem;
		left: 50%;
		transform: translate(-50%, 0);
		z-index: 4;
		box-shadow: 0 0 2rem rgba(0, 0, 0, 0.2);
		transition: var(--steady);
	}

	#cookies p {
		width: 500px;
		font-size: var(--paragraph);
		font-weight: var(--light);
		color: var(--black);
	}

	#cookies button {
		min-width: 100px;
		height: 40px;
		font-size: var(--paragraph);
		font-weight: var(--light);
		color: var(--white);
		background-color: var(--blue);
	}

	@media (width < 800px) {
		#cookies {
			width: 93%;
			min-height: 40px;
			height: auto;
			padding: 1rem 1rem;
			gap: 1.5rem;
		}

		#cookies p {
			font-size: 0.9rem;
		}

		#cookies button {
			min-width: 100px;
			height: 30px;
			font-size: 0.9rem;
		}
	}
</style>
