<script>
import axios from "axios";
import { store } from '../store'

export default {
    name: "PostList",
    components: {
    },
    data() {
        return {
            store,
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
            axios.get(this.store.apiUrl + "posts").then(response => {
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
                this.$router.push({ name: 'error', params: { code: 404 } })
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
                axios.get(this.store.apiUrl + "posts", config).then(response => {
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
                axios.get(this.store.apiUrl + "posts", config).then(response => {
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
                axios.get(this.store.apiUrl + "posts", config).then(response => {
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
                <h1>Post List</h1>

                <!-- POSTS -->
                <div class="row row-cols-1 row-cols-md-2 g-4 mb-4 ">
                    <div v-for="post in posts" class="col">
                        <div class="card h-100">
                            <img :src="store.storageUrl + post.image " class="card-img-top" alt="...">
                            <div class="card-body">
                                <h5>
                                    <router-link :to="{name:'single-post', params: {id: post.id} }" class="me-2">{{ post.title
                                                                }}</router-link>
                                </h5>
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

                <!-- NEXT PAGE -->
                <div class="row">
                    <div class="col d-flex justify-content-center align-items-center">
                        <a @click="getPostsPrevPage()" class="text-light btn btn-primary me-2">Previous page</a>
                        <a @click="getPostsPage(pageNumber)" v-for="pageNumber in postsTotalPages" class="text-light  btn btn-primary me-2">{{ pageNumber }}</a>
                        <a @click="getPostsNextPage()" class="text-light btn btn-primary">Next page</a>
                    </div>
                </div>
            </div>

        </section>

    </main>
</template>

<style scoped>
a {
    color: black;
}
</style>