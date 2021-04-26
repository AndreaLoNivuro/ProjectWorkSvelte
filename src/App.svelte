<script>
	import Router from 'svelte-spa-router'
	import { location, replace } from 'svelte-spa-router'
	import { wrap } from 'svelte-spa-router/wrap'
	import { afterUpdate } from 'svelte';

	let url
	url = $location;
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
		// '/login': Login,
		'/login': wrap({
			component: Login,
			guards: [userIsLogged()],
		}),
		'/registrati': Registra,
		// '/': Home,
		'/entrate': Entrate,
		'/uscite': Uscite,
		// '/inserisci': FormInput,
		'/inserisci/:id?': FormInput,
		'/dettaglio': DettaglioEntrateUscite,
		'/': wrap({
			component: Home,
			guards: [userIsNotLogged()],
            redirect: '/login'
		})
	}

	function userIsNotLogged() {
		if (sessionStorage.getItem('user') != null) {
			console.log("ok")
			return true
		}
		console.log("not ok")
		replace('/login')
		return false
	}

	function userIsLogged() {
		if (sessionStorage.getItem('user') == null) {
			return true
		}
		return false
	}

	afterUpdate(() => {
		console.log('the component just updated');
		url = $location;
    	console.log(url)
	});

	// const routes = [
	// 	{
	// 		name: '/',
	// 		component: Home,
	// 		onlyIf: { guard: userIsLogged, redirect: '/login' },
	// 	},
	// 	{ 
	// 		name: 'login',
	// 		component: Login 
	// 	},
	// 	{ 
	// 		name: '/registrati',
	// 		component: Registra 
	// 	},
	// 	{
	// 		name: 'entrate',
	// 		component: Entrate,
	// 		onlyIf: { guard: userIsLogged, redirect: '/login' },
	// 	},
	// 	]

</script>
{#if url != "/login" & url != "/registrati"}
	<nav><Menu></Menu></nav>
{/if}

<main>
	<Router {routes}/>
</main>