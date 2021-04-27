<script>
    import '../styleFile/profilo.css';

    let name = sessionStorage.getItem('name')
    let surname = sessionStorage.getItem('surname')
    let email = sessionStorage.getItem('user')
    let imageProfile = sessionStorage.getItem('imageProfile')
</script>

<!-- <h2 style="text-align:center">User Profile Card</h2> -->

<div class="card">
  <img src="{imageProfile}" alt="{name} {surname}" style="width:100%">
  <h1>{name} {surname}</h1>
  <p>Email</p>
  <p class="titleProfile">{email}</p>
  
  <!-- <p><button class="buttonProfile">Contact</button></p> -->
</div>
