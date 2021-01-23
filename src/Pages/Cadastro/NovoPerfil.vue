<template>
<div>
    <a class="nav-link" aria-current="page" href="#" @click="showModal = true">Novo Perfil</a>

    <div class="modal fade" :style="{display: showModal ? 'block' : 'none'}" :class="{show: showModal}">
      <div class="modal-dialog">
        <div class="modal-content">
            <div class="modal-body">
                <div class="form-group">
                    <input required type="text" class="form-control" placeholder="Nome" v-model="nome"/>
                </div>
                <div class="form-group">
                    <input required type="text" class="form-control" placeholder="Data de Nascimento" v-model="dtaNasc"/>
                </div>
            </div>
            <div class="modal-footer">
                <button type="button" class="btn btn-primary" @click="doCad()">Cadastrar</button>
                <button type="button" class="btn btn-secondary" @click="closeModal ()">Fechar</button>
            </div>
        </div>
      </div>
    </div>
</div>

</template>

<script>
import '../../firebase/index'
export default {
  data: () => {
    return {
      loading: false,
      nome: '',
      dtaNasc: '',
      showModal: false
    }
  },
  methods: {
    closeModal () {
      this.showModal = false
    },
    doCad () {
      this.loading = true
      this.loading = false

      const ref = this.$firebase.database().ref(`/${window.uid}`)
      const id = ref.push().key

      const DadoDbaCli = {
        id,
        v_nome: this.nome,
        v_dtaNasc: this.dtaNasc
      }

      ref.child(id).set(DadoDbaCli, err => {
        if (err) {
          console.log(err)
        }
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.form-login {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  .card {
    width: 25%;
  }
}
</style>
