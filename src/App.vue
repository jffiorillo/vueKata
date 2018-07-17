<template>
  <div id="app">
    <div class="header">
      <h1>Welcome to NASA!</h1>
    </div>
    <div class="row">
      <main-menu />
      <div class="main">
        <router-view/>
      </div>
    </div>
  </div>
</template>

<script>
import MainMenu from '@/components/MainMenu.vue'
export default {
  name: 'App',
  components: {
    'main-menu': MainMenu
  }
}
</script>

<style>
  .app {
    margin: auto;
  }
  .row {
    display: flex;
  }
  .menu {
    width: 200px;
  }
</style>
