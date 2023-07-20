<script>
import AppHeader from './components/AppHeader.vue';
// import AppMain from './components/AppMain.vue';
import AppFooter from './components/AppFooter.vue';


export default {
  name: 'App',
  components: {
    AppHeader,
    // AppMain,
    AppFooter
  },
  data() {
    return {
    }
  },
  methods: {

  },
  mounted() {
  }
}
</script>
<template>

  <header>
    <AppHeader />
  </header>

  <router-view></router-view>

  <footer>
    <AppFooter />
  </footer>

</template>

<style scoped>

</style>