<template>
<div>
    <a class="nav-link" aria-current="page" href="#" @click="showModal = true">Não possui Cadastro?</a>

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
                <div class="form-group">
                    <input required type="email" class="form-control" placeholder="E-mail" v-model="email"/>
                </div>
                <div class="form-group">
                    <input required type="password" class="form-control" placeholder="Senha" v-model="senha"/>
                </div>
                <div class="form-group">
                    <input required type="password" class="form-control" placeholder="Confirmar Senha" v-model="confSenha"/>
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
import firebase from 'firebase'
export default {
  data: () => {
    return {
      loading: false,
      nome: '',
      dtaNasc: '',
      email: '',
      senha: '',
      confSenha: '',
      showModal: false
    }
  },
  methods: {
    closeModal () {
      this.showModal = false
    },
    async doCad () {
      this.loading = true
      try {
        const res = await firebase.auth().createUserWithEmailAndPassword(this.email, this.senha)
        window.uid = res.user.uid

        console.log(res)
      } catch (err) {
        console.log(err)
      }
      this.loading = false

      const ref = this.$firebase.database().ref(window.uid)
      const id = ref.push().key

      const DadoDbaCli = {
        id,
        v_nome: this.nome,
        v_dtaNasc: this.dtaNasc,
        v_email: this.email,
        v_senha: this.senha
      }

      ref.child(id).set(DadoDbaCli, err => {
        if (err) {
          console.log(err)
        }
        {
          const res = this.firebase.auth().signInWithEmailAndPassword(this.email, this.senha)
          window.uid = res.user.uid
          this.$router.push({ name: 'Home' })
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
