<script>
    import {link} from 'svelte-spa-router'

    let name = sessionStorage.getItem('name')

    function logout() {
      sessionStorage.clear()
    }

</script>

<nav class="navbar navbar-expand-lg navbar-light bg-light">
    <a class="navbar-brand" href="/" use:link>{name}</a>
    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
  
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav mr-auto">
        <li class="nav-item active">
          <a class="nav-link" href="/" use:link>Home <span class="sr-only">(current)</span></a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="/entrate" use:link>Entrate</a>
        </li>
        <li class="nav-item">
            <a class="nav-link" href="/uscite" use:link>Uscite</a>
        </li>
      </ul>
      <ul class="navbar-nav" style="float:right; margin-right:10%">
        <li class="nav-item" style="float:right">
            <a class="nav-link" href="/profilo" use:link>Profilo</a>
        </li>
        <li class="nav-item" style="float:right">
            <a class="nav-link" href="/login" use:link on:click={logout}>Logout</a>
        </li>
      </ul>
    </div>
  </nav>