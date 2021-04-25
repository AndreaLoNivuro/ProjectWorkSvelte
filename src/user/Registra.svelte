<script>
    import { onMount } from 'svelte';
    import { link, push } from 'svelte-spa-router'
    import '../styleFile/user.css';
    import Api from '../Api.js';

    let allUser = []
    let errorLogin = ''

    let user = {
        email: '',
        name: '',
        surname: '',
        password: ''
    }

    onMount(async () => {
        const response = await Api.get('/user/findAll')
        allUser = response.result
    });

    function create() {
        console.log(user)
        for (let userDB of allUser) {
            if (userDB.email == user.email) {
                errorLogin = 'Email già esistente, se hai già un account, esegui il Login.'
            }
        }
        if (errorLogin == '') {
            Api.post('/user/create', user)
            .then((response) => sessionStorage.setItem('user', response.result.email));
        }
    }

</script>

<div class="container-contact2">
    <div class="wrap-contact2">
        <div class="titolo">
            Registrazione
        </div>
        <form class="contact2-form validate-form">
            <div class="wrap-input2 validate-input">
                <input type='email' placeholder='email' class="input2" bind:value={user.email}>
            </div>

            <div class="wrap-input2 validate-input" >
                <input type='text' placeholder='Nome' class="input2" bind:value={user.name}>
            </div>

            <div class="wrap-input2 validate-input">
                <input type='text' placeholder='Cognome' class="input2" bind:value={user.surname}>
            </div>

            <div class="wrap-input2 validate-input">
                <input type='password' placeholder='Password' class="input2" bind:value={user.password}>
            </div>

            <div class="radius-icon">
                <!-- svelte-ignore a11y-missing-attribute -->
                <a on:click={create}  class="btn btn-xs btn-info">
                    REGISTRATI
                </a>
            </div>
        </form>
        <!-- href="/" use:link -->
        <p>{errorLogin}</p>
        <h2>Hai già un profilo?</h2>
        <div class="radius-icon">
            <a href="/login" use:link class="btn btn-xs btn-info">
                LOGIN
            </a>
        </div>
    </div>
</div>