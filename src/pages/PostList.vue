<script>
import AppMain from '../components/AppMain.vue';


export default {
    name: "PostList",
    components: {
        AppMain
    },
    data() {
        return {
        }
    }
}
</script>

<template>

    <section>
        <div class="container">
            <div class="row">
                <div class="col">
                    <h1>Lista Posts</h1>
                </div>
            </div>
        </div>
        <AppMain />
    </section>

</template>

<style>

</style>