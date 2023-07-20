<script>
import axios from "axios";
import { store } from '../store'

export default {
    name: "SinglePost",

    data() {
        return {
            store,
            loading: false,
            loadingError: false,
            post: null
        }
    },
    methods: {
        getPost(id) {

            this.loading = true;
            axios.get(this.store.apiUrl + "posts/" + id).then(response => {
                console.log(response.data);
                this.post = response.data.results;
                this.loading = false;
            }).catch(err=>{
                this.loading = false;
                this.loadingError = err.message;
                this.$router.push({ name: 'error', params: { code: 404 } })
            });

        },
    },
    mounted() {
        this.getPost( this.$route.params.id )
    }
}

</script>

<template>

    <section v-if="post">
        <div class="container">
            <div class="row">
                <div class="col">
                    <h1>Lista Post</h1>
                </div>
            </div>
        </div>
        <div class="container">
            <div class="row">
                <div class="col">
                    <div class="card">

                        <img v-if="post.image" :src="store.storageUrl + post.image " class="card-img-top" alt="...">
                        <img v-else src="https://t3.ftcdn.net/jpg/02/48/42/64/360_F_248426448_NVKLywWqArG2ADUxDq6QprtIzsF82dMF.jpg" alt="">
                        <div class="card-body">
                            <h5 class="card-title">{{ post.title }}</h5>
                            <p class="card-text">{{ post.content }}</p>
                            <p class="card-text">Technology:
                                <ul v-if="post.technologies" v-for="technology in post.technologies">
                                    <li>{{ technology.name }}</li>
                                </ul>
                                <span v-else>Nessuna tecnologia selezionata</span>
                            </p>
                        </div>
                    </div>
                </div>
            </div>
        </div>


    </section>

</template>

<style>

</style>