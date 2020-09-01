<template>
  <div id="app">
    <marry />
  </div>
</template>

<script>
import Marry from './components/Marry.vue'

export default {
  name: 'App',
  components: {
    Marry
  }
}
</script>

<style lang="scss">
html,
body {
  height: 100%;
  padding: 0;
  margin: 0;
}
#app {
  height: 100%;
  color: #fff;
}
</style>
