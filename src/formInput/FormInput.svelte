<script>
    import Router from 'svelte-spa-router'
    import { location, push } from 'svelte-spa-router'
    import { onMount } from 'svelte';
    import { link } from 'svelte-spa-router'
    import '../styleFile/forminput.css';

    import dataApp from '../data.js';
    
    import Api from '../Api.js';

    const categorieEntrate = dataApp.categorieEntrate
    const categorieUscite = dataApp.categorieUscite
    const tipiMovimento = dataApp.tipo

    export const idUrl = $location.slice(11).toString();
    console.log(idUrl)

    let movement = {
        id: '',
        amount: '',
        category: '',
        description: '',
        type: '',
        id_utente: '',
        date: '',
    }

    if (idUrl != "") {
        onMount(async () => {
            const response = await Api.get('/movement/findAll')
            for (let movimento of response.result) {
                if (movimento.id == idUrl) {
                    movement.id = movimento.id
                    movement.amount = movimento.amount
                    movement.category = movimento.category
                    movement.description = movimento.description
                    movement.type = movimento.type
                    movement.id_utente = movimento.id_utente
                    movement.date = movimento.date
                }
            }
        });
    }

    function create() {
        Api.post('/movement/create', movement)
    }

    function deleteMovement(movement) {
        Api.post('/movement/delete', movement)
    }

</script>

<div class="container-contact2">
    <div class="wrap-contact2">
        <div class="titolo">
            AGGIUNGI MOVIMENTO
        </div>
        <form class="contact2-form validate-form">
            <div class="wrap-input2 validate-input">
                <input type='number' placeholder='Importo' class="input2" bind:value={movement.amount}>
            </div>

            <div class="wrap-input2 validate-input">
                <input type='date' placeholder='Data' class="input2" bind:value={movement.date}>
            </div>

            <div class="wrap-input2 validate-input">
                <select name="dropdown" class="input2" bind:value={movement.type}>
                    <option value="" selected>Tipo</option>
                    {#each tipiMovimento as tipo}
                        <option value={tipo}>{tipo.toUpperCase()}</option>
                    {/each}
                </select>
            </div>

            {#if movement.type != ""}
                <div class="wrap-input2 validate-input">
                    <select name="dropdown" class="input2" bind:value={movement.category}>
                        <option value="" selected>Categoria</option>
                        {#if movement.type == "entrata"}
                            {#each categorieEntrate as categoria}
                                <option value={categoria}>{categoria}</option>
                            {/each}
                        {:else if movement.type == "uscita"}
                            {#each categorieUscite as categoria}
                                <option value={categoria}>{categoria}</option>
                            {/each}
                        {/if}
                    </select>
                </div>
            {/if}

            <div class="wrap-input2 validate-input">
                <input type='textarea' placeholder='Descrizione' class="input2" bind:value={movement.description}>
            </div>

            <table style="width: 100%;">
                <tr>
                    <td>
                        <div class="radius-icon">
                            <a href="/" use:link class="btn btn-xs btn-info">
                                INDIETRO
                            </a>
                        </div>
                    </td>
                    {#if idUrl != ""}
                        <td>
                            <!-- href="/dettaglio" use:link -->
                            <div class="radius-icon">
                                <!-- svelte-ignore a11y-missing-attribute -->
                                <a on:click={deleteMovement(movement), () => push("/dettaglio") } class="btn btn-xs btn-info">
                                ELIMINA
                                </a>
                            </div>
                        </td>
                    {/if}
                    <td>
                        <div class="radius-icon">
                            <!-- svelte-ignore a11y-missing-attribute -->
                            <a class="btn btn-xs btn-info" href="/" use:link on:click={create}>
                                AGGIUNGI
                            </a>
                        </div>
                    </td>
                </tr>
            </table>

        </form>
    </div>
</div>