<script>
import axios from "axios";
import ProjectCard from './ProjectCard.vue';

export default {
    name: "AppMain",
    components: {
        ProjectCard
    },
    data() {
        return {
            apiUrl: "http://localhost:8000/api/",
            posts: [],
            loading: false,
            loadingError: false,
            postsCurrentPage: 0,
            postsTotalPages: 0
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
        getPostsNextPage() {

            if(this.postsCurrentPage < this.postsTotalPages) {

                let config = {
                    params: {
                        page: (this.postsCurrentPage + 1)
                    }
                }

                this.loading = true;
                axios.get(this.apiUrl + "posts", config).then(response => {
                    // console.log(response.data.results);
                    // this.posts = response.data.results; //non paginate
                    this.posts = response.data.results.data; // paginate
                    this.postsCurrentPage = response.data.results.current_page;
                    this.postsTotalPages = response.data.results.last_page;
                    this.loading = false
                }).catch(err=>{
                    this.loading = false;
                    // this.loadingError = "errore nel caricamento dei dati";
                    this.loadingError = err.message;
                    // console.log(err)
                })
            }
        },
        getPostsPrevPage() {

            if(this.postsCurrentPage > 1) {
            
                let config = {
                    params: {
                        page: (this.postsCurrentPage - 1)
                    }
                }
            
                this.loading = true;
                axios.get(this.apiUrl + "posts", config).then(response => {
                    // console.log(response.data.results);
                    // this.posts = response.data.results; //non paginate
                    this.posts = response.data.results.data; // paginate
                    this.postsCurrentPage = response.data.results.current_page;
                    this.postsTotalPages = response.data.results.last_page;
                    this.loading = false
                }).catch(err=>{
                    this.loading = false;
                    // this.loadingError = "errore nel caricamento dei dati";
                    this.loadingError = err.message;
                    // console.log(err)
                })
            }
        },
        getPostsPage(pageNumber) {

            if (this.postsCurrentPage == pageNumber ) {
                
            } else {

                let config = {
                    params: {
                        page: (pageNumber)
                    }
                }
            
                this.loading = true;
                axios.get(this.apiUrl + "posts", config).then(response => {
                    // console.log(response.data.results);
                    // this.posts = response.data.results; //non paginate
                    this.posts = response.data.results.data; // paginate
                    this.postsCurrentPage = response.data.results.current_page;
                    this.postsTotalPages = response.data.results.last_page;
                    this.loading = false
                }).catch(err=>{
                    this.loading = false;
                    // this.loadingError = "errore nel caricamento dei dati";
                    this.loadingError = err.message;
                    // console.log(err)
                })

            }
            
        }
    },
    mounted() {
        this.getPosts();
    }
}
</script>
<template>

    <main>

        <!-- LOADING -->
        <section v-if="loading">
            <div class="container text-center mt-4">loading...</div> 
        </section>

        <!-- LOADING ERROR -->
        <section v-else-if="loadingError">
            <div class="container text-center mt-4">{{ loadingError }}</div> 
        </section>

        <!-- LOADING DONE -->
        <section v-else>

            <div class="container mt-4">

                <!-- POSTS -->
                <ProjectCard />

                <!-- NEXT PAGE -->
                <div class="row">
                    <div class="col d-flex justify-content-center align-items-center">
                        <a @click="getPostsPrevPage()" class="btn btn-primary me-2">Previous page</a>
                        <a @click="getPostsPage(pageNumber)" v-for="pageNumber in postsTotalPages" class="btn btn-primary me-2">{{ pageNumber }}</a>
                        <a @click="getPostsNextPage()" class="btn btn-primary">Next page</a>
                    </div>
                </div>
            </div>

        </section>

    </main>

</template>

<style scoped>

</style>