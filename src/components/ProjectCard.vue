<script>
import axios from "axios";
export default {
    name: 'ProjectCard',
    data() {
        return {
            apiUrl: "http://localhost:8000/api/",
            posts: [],
        }
    },
    methods: {
        getPosts() {
            this.loading = true;
            axios.get(this.apiUrl + "posts").then(response => {
                // console.log(response.data.results);
                // this.posts = response.data.results; //non paginate
                this.posts = response.data.results.data; // paginate
                this.postsCurrentPage = response.data.results.current_page;
                this.postsTotalPages = response.data.results.last_page;
                this.loading = false;
            }).catch(err=>{
                this.loading = false;
                // this.loadingError = "errore nel caricamento dei dati";
                this.loadingError = err.message;
                // console.log(err)
            })
        },
    },
    mounted() {
        this.getPosts();
    }
    
}
</script>

<template>

<div class="row row-cols-1 row-cols-md-2 g-4 mb-4">
    <div v-for="post in posts" class="col">
        <div class="card h-100">
            <!-- <img src="..." class="card-img-top" alt="..."> -->
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

</template>

<style scoped>

</style>