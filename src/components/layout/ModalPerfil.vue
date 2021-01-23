<template>
<div>
    <a class="nav-link" aria-current="page" href="#" @click="showModal = true">Perfil</a>

    <div class="modal fade" :style="{display: showModal ? 'block' : 'none'}" :class="{show: showModal}">
      <div class="modal-dialog">
        <div class="modal-content">
        <div class="modal-header">
            <h5 class="modal-title">Logado como, </h5> <div class="nome"></div>
        </div>
        <div class="modal-body">
            <p>Modal body text goes here.</p>
            <button type="button" class="btn btn-secondary" @click="cadNovoPerfil ()">Novo Perfil</button>
        </div>
        <novo-perfil/>
        <div class="modal-footer">
            <button type="button" class="btn btn-secondary" @click="closeModal ()">Fechar</button>
            <button type="button" class="btn btn-danger" @click="Logout()">Sair</button>
        </div>
        </div>
      </div>
    </div>

    <div class="modal-backdrop fade" :style="{display: showModal ? 'block' : 'none'}" :class="{show: showModal}"></div>
</div>
</template>

<script>
import '../../firebase/index'
import NovoPerfil from '../../Pages/Cadastro/NovoPerfil'
export default {
  components: { NovoPerfil },
  data: () => ({ showModal: false }),
  created () {

  },
  methods: {
    closeModal () {
      this.showModal = false
    },
    async Logout () {
      this.$root.$emit('Spinner::show')

      await this.$firebase.auth().signOut()

      this.$router.push({ name: 'Login' })

      this.$root.$emit('Spinner::hide')
    },
    getData () {
      const ref = this.$firebase.database().ref(`/${window.uid}`)
      ref.on('v_nome', data => {
        const nome = data.val()
        this.perfil = Object.keys(nome).map(i => nome[i])
        console.log(this.perfil)
        console.log(nome)
      })
    }
  }
}
</script>

<style scoped>

</style>
