<script>
import axios from "axios";
export default {
    name: "AppMain",
    data() {
        return {
            apiUrl: "http://localhost:8000/api/",
            posts: []
        }
    },
    methods: {
    },
    mounted() {
        axios.get(this.apiUrl + "posts").then(response => {
            console.log(response.data.results);
            this.posts = response.data.results;
        })
    }
}
</script>
<template>
    <main>
        <div class="container">
    
            <div class="card my-4 p-4" v-for="post in posts">
                <h1>{{ post.title }}</h1>
                <h3>Description: {{ post.content }}</h3>
                <h4>Technology:
                    <span v-if="post.technology" v-for="technology in post.technologies">{{technology.name }}</span>
                    <span v-else>Nessuna tecnologia selezionata</span>
                </h4>
            </div>
        </div>
    </main>
</template>