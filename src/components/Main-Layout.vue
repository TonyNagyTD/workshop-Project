<template>
  <header>
    <div class="banner">
      <!-- <img class="banner__image" :src="bannerImage" alt="Header image" /> -->
    </div>
    </header>
    <section>
      <ListComponent />
    </section>
</template>

<script>
import ListComponent from './list_component/List-component.vue'

export default {
  name: 'MainLayout',
  components: {
    ListComponent
  },
  props: {
  },
  data () {
    return {
      bannerImage: require('../assets/imgs/banner-header.jpg')
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  @import "./Main-Layout.scss";
</style>
