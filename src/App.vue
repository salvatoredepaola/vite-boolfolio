<script>
import AppHeader from './components/AppHeader.vue';
import AppMain from './components/AppMain.vue';
import AppFooter from './components/AppFooter.vue';


export default {
  name: 'App',
  components: {
    AppHeader,
    AppMain,
    AppFooter
  },
  data() {
    return {
    }
  },
  methods: {
    getPost() {
      axios.get(this.apiUrl + "posts").then(response => {
        console.log(response.data.results);
        this.posts = response.data.results;
      })
    }
  },
  mounted() {
  }
}
</script>
<template>
  <AppHeader />
  <AppMain />
  <AppFooter />
</template>
<style scoped>

</style>