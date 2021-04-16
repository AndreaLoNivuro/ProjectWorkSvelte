<script>
    import { location } from 'svelte-spa-router'
    import { onMount } from 'svelte';
    import { link } from 'svelte-spa-router'
    import '../styleFile/login.css';
    import '../styleFile/util.css';

    // let movement = {
    //     id: '',
    //     amount: '',
    //     category: '',
    //     description: '',
    //     type: '',
    //     id_utente: '',
    //     date: '',
    // }

    // import Api from '../Api.js';

    // if (idUrl != "") {
    //     onMount(async () => {
    //         const response = await Api.get('/movement/findAll')
    //         for (let movimento of response.result) {
    //             if (movimento.id == idUrl) {
    //                 movement.id = movimento.id
    //                 movement.amount = movimento.amount
    //                 movement.category = movimento.category
    //                 movement.description = movimento.description
    //                 movement.type = movimento.type
    //                 movement.id_utente = movimento.id_utente
    //                 movement.date = movimento.date
    //             }
    //         }
    //     });
    // }

    // function create() {
    //     Api.post('/movement/create', movement)
    // }

</script>

<div class="limiter">
    <div class="container-login100" style="background-image: url('');">
        <div class="wrap-login100">
            <form class="login100-form validate-form">
                <div class="wrap-input100 validate-input m-b-10" data-validate = "Username is required">
                    <input class="input100" type="text" name="username" placeholder="Username">
                    <span class="focus-input100"></span>
                    <span class="symbol-input100">
                        <i class="fa fa-user"></i>
                    </span>
                </div>

                <div class="wrap-input100 validate-input m-b-10" data-validate = "Password is required">
                    <input class="input100" type="password" name="pass" placeholder="Password">
                    <span class="focus-input100"></span>
                    <span class="symbol-input100">
                        <i class="fa fa-lock"></i>
                    </span>
                </div>

                <div class="container-login100-form-btn p-t-10">
                    <button class="login100-form-btn">
                        Login
                    </button>
                </div>

                <div class="text-center w-full">
                    <a class="txt1" href="/" use:link>
                        Create new account
                        <i class="fa fa-long-arrow-right"></i>						
                    </a>
                </div>
            </form>
        </div>
    </div>
</div>

<!-- <div class="container-contact2">
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
</div> -->