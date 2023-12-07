<template>
  <MainLayout />
</template>

<script>
import MainLayout from './components/Main-Layout.vue'

export default {
  name: 'App',
  components: {
    MainLayout
  }
}
</script>

<style lang="scss">
#app {
  overflow: hidden;
  background-color: hsl(180, 52%, 96%);
}
</style>
