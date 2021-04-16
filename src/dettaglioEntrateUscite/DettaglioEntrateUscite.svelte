<script>
  import { onMount } from 'svelte';
  import { link } from 'svelte-spa-router'

  import '../styleFile/dettaglio.css';

  import Api from '../Api.js';

  let rows = []
  let columns = ["Tipo", "Importo", "Categoria", "Descrizione", "Data"]

  onMount(async () => {
  const response = await Api.get('/movement/findAll')

      rows = response.result
	});

  function deleteMovement(movimento) {
    Api.post('/movement/delete', movimento)
  }
</script>
<table>
    <tr>
        {#each columns as nome}
          <th scope="col">{ nome }</th>
        {/each}
        <th></th>
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
            <td>
              <div class="radius-icon">
                <!-- svelte-ignore a11y-missing-attribute -->
                <a on:click={deleteMovement(movimento)} class="btn btn-xs btn-info">
                  Elimina
                </a>
              </div>
            </td>
        </tr>
    {/each}
</table>

