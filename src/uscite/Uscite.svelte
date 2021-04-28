<script>
    import { onMount } from 'svelte';
    import SvelteTable from "svelte-table";
    import UsciteChart from "./UsciteChart.svelte";
    import { afterUpdate } from 'svelte';

    import {link} from 'svelte-spa-router'

    import '../styleFile/entrateuscite.css';

    import Api from '../Api.js';

    let dataInizioString;
	let dataFineString;

    let rows = []
    let columns = ["Tipo", "Importo", "Categoria", "Descrizione", "Data"]

    onMount(async () => {
        dataInizioString = sessionStorage.getItem('dataInizio');
	    dataFineString = sessionStorage.getItem('dataFine');

		const response = await Api.get('/movement/findAll')

        rows = response.result.filter(movimento => {
          if (movimento.idUtente == sessionStorage.getItem('user')) {
            if (movimento.type === "uscita") {
              if (movimento.date >= dataInizioString & movimento.date <= dataFineString) {
                return movimento
              }
            }
          }
        })
    });

    afterUpdate(() => {
      sessionStorage.setItem('dataFine', dataFineString);
      sessionStorage.setItem('dataInizio', dataInizioString);
    });
</script>

<div class="grid-container2">
    <div class="button">
      <div class="radius-icon">
        <a href="/" use:link class="btn btn-xs btn-info">
          MOSTRA RIEPILOGO
        </a>
      </div>
        <!-- <button>MOSTRA RIEPILOGO</button> -->
    </div>
    <div class="side fixed">
      <div class="chart titolo">
        <UsciteChart></UsciteChart>
      </div>
      <div class="date">
        <div class="inizio titolo2">
            Data inizio
        </div>
        <div class="fine titolo2">
            Data fine
        </div>
        <div class="inputInizio wrapinput6">
            <input type="date" class="input6" bind:value={dataInizioString}>
        </div>
        <div class="inputFine wrapinput6">
            <input type="date" class="input6" bind:value={dataFineString}>
        </div>
      </div>
    </div>
    <div class="table tableWidth">
        <table>
            <tr>
                {#each columns as nome}
                  <th scope="col">{ nome }</th>
                {/each}
                <th></th>
            </tr>
            {#each rows as movimento}
                <tr>
                    <td>{ movimento.type }</td>
                    <td>{ movimento.amount }</td>
                    <td>{ movimento.category }</td>
                    <td>{ movimento.description }</td>
                    <td>{ movimento.date }</td>
                    <td>
                      <div class="radius-icon">
                        <a href="/inserisci/{movimento.id}" use:link class="btn btn-xs btn-info">
                          Modifica
                        </a>
                      </div>
                    </td>
                </tr>
            {/each}
        </table>
    </div>
  </div>