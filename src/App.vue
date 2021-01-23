<template>
  <div id="app">
    <base-spinner/>
    <div class="container-fluid" v-if="isLogged">
      <layout-navigation/>
      <router-view/>
    </div>
    <router-view v-else/>
  </div>
</template>

<script>
import './firebase/index'
import firebase from 'firebase'
import BaseSpinner from './components/global/BaseSpinner'
import LayoutNavigation from './components/layout/LayoutNavigation'
export default {
  name: 'App',
  components: {
    BaseSpinner,
    LayoutNavigation
  },
  data: () => ({ isLogged: false }),
  mounted () {
    firebase.auth().onAuthStateChanged(user => {
      window.uid = user ? user.uid : null
      this.isLogged = !!user

      console.log(window.uid)

      if (window.uid) {
        this.$router.push({ name: 'Home' })
      } else {
        this.$router.push({ name: 'Login' })
      }
      this.$root.$emit('Spinner::hide')
    })
  }
}
</script>

<style lang="scss">
#app {
  min-height: 100vh;
}
</style>
