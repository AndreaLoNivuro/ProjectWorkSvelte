<script>
    import { onMount } from 'svelte';
    import { link } from 'svelte-spa-router'
    import '../styleFile/user.css';
</script>

<div class="container-contact2">
    <div class="wrap-contact2">
        <div class="titolo">
            Login
        </div>
        <form class="contact2-form validate-form">
            <div class="wrap-input2 validate-input" data-validate="Name is required">
                <input type='number' placeholder='Importo' class="input2">
            </div>

            <div class="wrap-input2 validate-input" data-validate = "Valid email is required: ex@abc.xyz">
                <input type='text' placeholder='NAME' class="input2">
            </div>

            <div class="wrap-input2 validate-input" data-validate = "Valid email is required: ex@abc.xyz">
                <input type='text' placeholder='SURNAME' class="input2">
            </div>

            <div class="wrap-input2 validate-input" data-validate = "Valid email is required: ex@abc.xyz">
                <input type='password' placeholder='PASSWORD' class="input2">
            </div>

            <table style="width: 100%;">
                <tr>
                    <td>
                        <div class="container-contact2-form-btn">
                            <div class="wrap-contact2-form-btn">
                                <div class="radius-icon">
                                    <a href="/" class="btn btn-xs btn-info">
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
                                    <a href="/inserisci" class="btn btn-xs btn-info">
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