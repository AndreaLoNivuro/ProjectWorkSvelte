<script>
	import Router from 'svelte-spa-router'
	import { location, replace } from 'svelte-spa-router'
	import { wrap } from 'svelte-spa-router/wrap'
	import { afterUpdate } from 'svelte';
	import { onMount } from 'svelte';
	
	import './styleFile/app.css';
	
	import Menu from './menu/Menu.svelte';
	import Home from './home/Home.svelte';
	import Entrate from './entrate/Entrate.svelte';
	import Uscite from './uscite/Uscite.svelte';
	import FormInput from './formInput/formInput.svelte';
	import DettaglioEntrateUscite from './dettaglioEntrateUscite/DettaglioEntrateUscite.svelte';
	import Login from './user/Login.svelte';
	import Registra from './user/Registra.svelte';


	let url
	url = $location;
    console.log(url)

	let now = new Date(), monthInizio, dayInizio, yearInizio, monthFine, dayFine, yearFine;
	let dataInizioString;
	let dataFineString;
	
	const routes = {
		// '/login': Login,
		// '/registrati': Registra,
		// '/': Home,
		// '/entrate': Entrate,
		// '/uscite': Uscite,
		// '/inserisci/:id?': FormInput,
		// '/dettaglio': DettaglioEntrateUscite,
		'/login': wrap({
			component: Login,
			guards: [userIsLogged()],
		}),
		'/registrati': wrap({
			component: Registra,
			guards: [userIsLogged()],
		}),
		'/': wrap({
			component: Home,
			guards: [userIsNotLogged()],
            redirect: '/login'
		}),
		'/entrate': wrap({
			component: Entrate,
			guards: [userIsNotLogged()],
            redirect: '/login'
		}),
		'/uscite': wrap({
			component: Uscite,
			guards: [userIsNotLogged()],
            redirect: '/login'
		}),
		'/inserisci/:id?': wrap({
			component: FormInput,
			guards: [userIsNotLogged()],
            redirect: '/login'
		}),
		'/dettaglio': wrap({
			component: DettaglioEntrateUscite,
			guards: [userIsNotLogged()],
            redirect: '/login'
		}),
	}

	onMount(async () => {
		monthFine = '' + (now.getMonth() + 1),
        dayFine = '' + now.getDate(),
        yearFine = now.getFullYear();

		monthInizio = '' + (now.getMonth() + 1),
        dayInizio = '1',
        yearInizio = now.getFullYear();

		if (monthFine.length < 2) 
			monthFine = '0' + monthFine;
		if (dayFine.length < 2) 
			dayFine = '0' + dayFine;

		if (monthInizio.length < 2) 
			monthInizio = '0' + monthInizio;
		if (dayInizio.length < 2) 
			dayInizio = '0' + dayInizio;

		dataFineString = [yearFine, monthFine, dayFine].join('-');
		sessionStorage.setItem('dataFine', dataFineString);
		dataInizioString = [yearInizio, monthInizio, dayInizio].join('-');
		sessionStorage.setItem('dataInizio', dataInizioString);
	});

	function userIsNotLogged() {
		if (sessionStorage.getItem('user') != null) {
			return true
		}
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

</script>
{#if url != "/login" & url != "/registrati"}
	<nav><Menu></Menu></nav>
{/if}

<main>
	<Router {routes}/>
</main>