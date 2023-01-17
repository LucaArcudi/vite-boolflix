<script>
import { store } from "../store"

import axios from "axios"

export default {
    name: "AppHeader",
    data() {
        return {
            store,
            apiUri: "https://api.themoviedb.org/3/search/",
            apiKey: "000338f49db5f35b4ac8f836f4766eac",
            userSearch: "",
        }
    },
    methods: {
        getMoviesOrSeries(apiResource) {
            axios.get(this.apiUri + apiResource, {
                params: {
                    api_key: this.apiKey,
                    language: "it-IT",
                    query: this.userSearch,

                }
            })
                .then((response) => {
                    console.log(response.data.results);
                    if (apiResource === "movie") {
                        this.store.moviesList = response.data.results;
                    } else {
                        this.store.seriesList = response.data.results;
                    }

                })
                .catch(function (error) {
                    console.log(error);
                })
                .then(function () {

                });
        },

        getResource() {
            this.getMoviesOrSeries("movie");
            this.getMoviesOrSeries("tv")
        }


    },

}
</script>

<template>
    <header>
        <input v-model="userSearch" type="text" placeholder="Search for a movie or a TVs">
        <button @click="getResource()">Search</button>
    </header>
</template>

<style lang="scss" scoped>

</style>



