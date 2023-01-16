<script>
import { store } from "../store"

import axios from "axios"

export default {
    name: "AppHeader",
    data() {
        return {
            store,
            apiUri: "https://api.themoviedb.org/3/search/movie",
            apiKey: "000338f49db5f35b4ac8f836f4766eac",
            userSearch: "",
        }
    },
    methods: {
        getMovies() {
            axios.get(this.apiUri, {
                params: {
                    api_key: this.apiKey,
                    language: "it-IT",
                    query: this.userSearch,

                }
            })
                .then((response) => {
                    console.log(response.data.results);
                    this.store.moviesList = response.data.results;
                })
                .catch(function (error) {
                    console.log(error);
                })
                .then(function () {

                });
        }
    },

}
</script>

<template>
    <header>
        <input v-model="userSearch" type="text" placeholder="Search for a movie or a TVs">
        <button @click="getMovies()">Search</button>
    </header>
</template>

<style lang="scss" scoped>

</style>



