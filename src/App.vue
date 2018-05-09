<template>
  <div id="app">
    <nav-bar />
    <div class="container">
      <div class="col-sm-10 offset-sm-1">
        <router-view />
      </div>
    </div>
  </div>
</template>

<script>
import NavBar from './components/NavBar.vue'

export default {
  name: 'app',
  components: {
    NavBar
  }
}
</script>

<style lang="scss">
@import '../node_modules/bootstrap/scss/bootstrap.scss';
</style>
