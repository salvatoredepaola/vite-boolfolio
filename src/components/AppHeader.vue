<script>
export default {
  name: 'AppHeader',
  data() {
    return {
      navLinks: [
        { label: "Home", to: { name: "home" } },
        { label: "About us", to: { name: "about" } },
        { label: "Posts", to: { name: "posts" } },
        { label: "Errore", to: { name: "error", params: { code: "404"} } },
      ]
    }
  }
}
</script>

<template>

  <section>
    <div class="container-fluid p-4 bg-dark">
      <div class="container">
        <div class="row">
            <div class="col">

              <template v-for="link in navLinks">
                <router-link :to="link.to" class="text-light me-2">{{ link.label }}</router-link>
              </template>

              <!-- <router-link :to="{name: 'home'}">Home</router-link>
              <router-link :to="{name: 'about'}">Home</router-link>
              <router-link :to="{name: 'posts'}">Home</router-link> -->


                <!-- <a href="/">Home</a>
                <a href="/about-us">About us</a>
                <a href="/posts">Post</a> -->
            </div>
        </div>
      </div>
    </div>
  </section>
    
</template>


<style scoped>

</style>