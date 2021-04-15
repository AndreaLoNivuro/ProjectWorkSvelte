<script>
	import { link } from 'svelte-spa-router'

	import EntrateChart from '../entrate/EntrateChart.svelte';
	import UsciteChart from '../uscite/UsciteChart.svelte';
	import RisparmioChart from '../risparmio/RisparmioChart.svelte';

	import { onMount } from 'svelte';
	import Api from '../Api.js';

	import '../styleFile/home.css';

	export let size = "5em";
	export let width = size;
	export let height = size;
	export let color = "black";
	export let viewBox = "0 0 24 24";

	let totEntrate = 0;
	let totUscite = 0;

	onMount(async () => {
		const response = await Api.get('/movement/findAll')
		
		response.result.filter(movimento => {
            if (movimento.type === "entrata") {
                totEntrate += movimento.amount;
            } else if (movimento.type === "uscita") {
				totUscite += movimento.amount;
			}
        })
	});
</script>


<div class="grid-container">
	<div class="date">
		<div class="inizio titolo2">
			Data inizio
		</div>
		<div class="fine titolo2">
			Data fine
		</div>
		<div class="inputInizio wrap-input3">
			<input type="date" class="input3">
		</div>
		<div class="inputFine wrap-input3">
		<input type="date" class="input3">
		</div>
	</div>
	<div class="bottoni">
		<div class="inserisci">
			<div class="radius-icon">
				<a href="/inserisci" use:link class="btn btn-xs btn-info">
					Inserisci movimento
				</a>
			</div>
		</div>
		<div class="dettaglio">
			<div class="radius-icon">
				<a href="/dettaglio" use:link class="btn btn-xs btn-info">
					Dettaglio movimenti
				</a>
			</div>
		</div>
	</div>
	<div class="titoloEntrate titolo">
		Entrate
	</div>
	<div class="titoloUscite titolo">
		Uscite
	</div>
	<div class="importoEntrate titolo">
		{ totEntrate } €
	</div>
	<div class="ImportoUscite titolo">
		{ totUscite } €
	</div>
	<div class="graficoEntrate">
		<EntrateChart></EntrateChart>
	</div>
	<div class="graficoUscite">
		<UsciteChart></UsciteChart>
	</div>
	<div class="freccia">
		<svg width="{width}" height="{height}" viewBox="{viewBox}"><path d="M11,16H3V8H11V2L21,12L11,22V16M13,7V10H5V14H13V17L18,12L13,7Z" fill="{color}"/></svg>
	</div>
	<div class="titoloRisparmio titolo">
		Risparmio
	</div>
	<div class="importoRisparmio titolo">
		{ totEntrate - totUscite } €
	</div>
	<div class="graficoRisparmio">
		<RisparmioChart></RisparmioChart>
	</div>
</div>
