<script>
    import { location, replace, push } from 'svelte-spa-router'
    import { onMount } from 'svelte';
    import { link } from 'svelte-spa-router'
    import '../styleFile/login.css';
    import '../styleFile/util.css';
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

    function login() {
        console.log(user)
        for (let userDB of allUser) {
            if (userDB.email == user.email) {
                if (userDB.password == user.password){
                    sessionStorage.setItem('user', userDB.email);
                    sessionStorage.setItem('name', userDB.name);
                    sessionStorage.setItem('surname', userDB.surname);
                    sessionStorage.setItem('imageProfile', userDB.imageProfile);
                    replace('/')
                } else {
                    errorLogin = 'Password errata.'
                }
            }
        }
        if (sessionStorage.getItem('user') == null) {
            errorLogin = 'Email o password errata.'
        }
    }

</script>

<div class="container-contact2">
    <div class="wrap-contact2">
        <div class="titolo">
            Login
        </div>
        <form class="contact2-form validate-form">
            <div class="wrap-input2 validate-input">
                <input type='email' placeholder='email' class="input2" bind:value={user.email}>
            </div>

            <div class="wrap-input2 validate-input">
                <input type='password' placeholder='Password' class="input2" bind:value={user.password}>
            </div>

            <div class="radius-icon">
                <!-- svelte-ignore a11y-missing-attribute -->
                <a on:click={login}  class="btn btn-xs btn-info">
                    LOGIN
                </a>
            </div>
        </form>
        <!-- href="/" use:link -->
        <p>{errorLogin}</p>
        <h2>Non hai ancora un profilo?</h2>
        <div class="radius-icon">
            <a href="/registrati" use:link class="btn btn-xs btn-info">
                REGISTRATI
            </a>
        </div>
    </div>
</div>