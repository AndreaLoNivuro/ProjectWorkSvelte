<script>
    import { location } from 'svelte-spa-router'
    import { onMount } from 'svelte';
    import { link } from 'svelte-spa-router'
    import '../styleFile/forminput.css';

    import dataApp from '../data.js';

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

    import Api from '../Api.js';

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
                        <div class="container-contact2-form-btn">
                            <div class="wrap-contact2-form-btn">
                                <div class="radius-icon">
                                    <a href="/" use:link class="btn btn-xs btn-info">
                                        INDIETRO
                                    </a>
                                </div>
                            </div>
                        </div>
                    </td>
                    <td>
                        <div class="container-contact2-form-btn">
                            <div class="wrap-contact2-form-btn">
                                <!-- <div class="contact2-form-bgbtn"></div>
                                <button class="contact2-form-btn" type="submit">
                                    AGGIUNGI
                                </button> -->
                                <div class="radius-icon">
                                    <a href="/" use:link class="btn btn-xs btn-info" on:click={create}>
                                        AGGIUNGI
                                    </a>
                                </div>
                            </div>
                        </div>
                    </td>
                </tr>
            </table>

        </form>
    </div>
</div>


<!-- <form on:submit|preventDefault={create}>
    <div class="container">
        <div class="row">
            <div class="col-md-12">
                <div class="well well-sm">
                    <form class="form-horizontal" method="post">
                        <fieldset>
                            <legend class="text-center header">Contact us</legend>

                            <div class="form-group">
                                <span class="col-md-1 col-md-offset-2 text-center"><i class="fa fa-user bigicon"></i></span>
                                <div class="col-md-8">
                                    <input id="fname" name="name" type="text" placeholder="First Name" class="form-control">
                                </div>
                            </div>
                            <div class="form-group">
                                <span class="col-md-1 col-md-offset-2 text-center"><i class="fa fa-user bigicon"></i></span>
                                <div class="col-md-8">
                                    <input id="lname" name="name" type="text" placeholder="Last Name" class="form-control">
                                </div>
                            </div>

                            <div class="form-group">
                                <span class="col-md-1 col-md-offset-2 text-center"><i class="fa fa-envelope-o bigicon"></i></span>
                                <div class="col-md-8">
                                    <input id="email" name="email" type="text" placeholder="Email Address" class="form-control">
                                </div>
                            </div>

                            <div class="form-group">
                                <span class="col-md-1 col-md-offset-2 text-center"><i class="fa fa-phone-square bigicon"></i></span>
                                <div class="col-md-8">
                                    <input id="phone" name="phone" type="text" placeholder="Phone" class="form-control">
                                </div>
                            </div>

                            <div class="form-group">
                                <span class="col-md-1 col-md-offset-2 text-center"><i class="fa fa-pencil-square-o bigicon"></i></span>
                                <div class="col-md-8">
                                    <textarea class="form-control" id="message" name="message" placeholder="Enter your massage for us here. We will get back to you within 2 business days." rows="7"></textarea>
                                </div>
                            </div>

                            <div class="form-group">
                                <div class="col-md-12 text-center">
                                    <button type="submit" class="btn btn-primary btn-lg">AGGIUNGI</button>
                                </div>
                            </div>
                        </fieldset>
                    </form>
                </div>
            </div>
        </div>
    </div>
</form> -->