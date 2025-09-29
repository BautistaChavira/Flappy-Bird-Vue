<template>
  <div class="container">
    <Game />
  </div>
</template>

<script>
  import Game from './components/Game.vue'
  export default {
    components: { Game }
  }
</script>

<style>
  .container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background: #222;
  }
</style>