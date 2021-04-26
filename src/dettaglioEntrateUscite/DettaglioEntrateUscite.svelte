<script>
  import { onMount } from 'svelte';
  import { link } from 'svelte-spa-router'

  import '../styleFile/dettaglio.css';

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
          if (movimento.date >= dataInizioString & movimento.date <= dataFineString) {
            return movimento
          }
        }
      })
	});
</script>
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

