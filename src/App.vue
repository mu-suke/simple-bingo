<template>
  <div id="app" v-cloak>
    <Bingo></Bingo>
  </div>
</template>

<script>
import Bingo from './components/Bingo'

export default {
  name: 'app',
  components: {
    Bingo
  }
}
</script>

<style lang="scss">

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

</style>

// kebab-case