<template>
<nav class="navbar navbar-expand-lg navbar-light bg-light">
  <div class="container-fluid">
    <a class="navbar-brand" href="#">CinePrjct</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavAltMarkup" aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
      <div class="navbar-nav">
        <a class="nav-link" aria-current="page" href="#">Minha Lista</a>
        <modal-perfil/>
      </div>
    </div>
  </div>
</nav>
</template>

<script>
import ModalPerfil from './ModalPerfil'
export default {
  components: { ModalPerfil },
  computed: {
    routerLinks () {
      return this.$router.options.routers.filter(r => r.name !== 'login') // maybe
    }
  }

}
</script>

<style>

</style>
