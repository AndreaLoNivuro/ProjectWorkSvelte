<script>
	import Router from 'svelte-spa-router'
	import { location } from 'svelte-spa-router'

	export const url = $location;
    console.log(url)

	import './styleFile/app.css';

	import Menu from './menu/Menu.svelte';
	import Home from './home/Home.svelte';
	import Entrate from './entrate/Entrate.svelte';
	import Uscite from './uscite/Uscite.svelte';
	import FormInput from './formInput/formInput.svelte';
	import DettaglioEntrateUscite from './dettaglioEntrateUscite/DettaglioEntrateUscite.svelte';
	import Login from './user/Login.svelte';
	import Registra from './user/Registra.svelte';
	
	const routes = {
		// Exact path
		'/login': Login,
		'/registrati': Registra,
		'/': Home,
		'/entrate': Entrate,
		'/uscite': Uscite,
		// '/inserisci': FormInput,
		'/inserisci/:id?': FormInput,
		'/dettaglio': DettaglioEntrateUscite,
	}

</script>
{#if url != "/login" & url != "/registrati"}
	<nav><Menu></Menu></nav>
{/if}

<main>
	<Router {routes}/>
</main>

<!-- <style>
	body {
		padding: 0;
	}
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin-top: 15%;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}

	nav {
		position: fixed;
		width: 100%;
	}
</style> -->