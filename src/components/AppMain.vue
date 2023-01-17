<script>
import { store } from "../store"

export default {
    name: "AppMain",
    data() {
        return {
            store,
            myFlags: ["en", "es", "fr", "it"]
        }
    },

    methods: {
        getImagePath: function (imgPath) {
            return new URL(`../assets/img/${imgPath}.png`, import.meta.url).href;
        }
    }
}
</script>

<template>
    <main>
        <ul>
            <li v-for="movie in store.moviesList">
                <ul>
                    <li>
                        <h3>Titolo: {{ movie.title }}</h3>
                    </li>
                    <li>
                        <h4>Titolo originale: {{ movie.original_title }}</h4>
                    </li>
                    <li>
                        <p>
                            Lingua: <img v-if="myFlags.includes(movie.original_language)"
                                :src="getImagePath(movie.original_language)" alt="flags">
                            <span v-else>{{ movie.original_language }}</span>
                        </p>
                    </li>
                    <li>
                        <span>Voto: {{ movie.vote_average }}/10</span>
                    </li>
                </ul>
            </li>
            <li v-for="serie in store.seriesList">
                <ul>
                    <li>
                        <h3>Titolo: {{ serie.name }}</h3>
                    </li>
                    <li>
                        <h4>Titolo originale: {{ serie.original_name }}</h4>
                    </li>
                    <li>
                        <p>
                            Lingua: <img v-if="myFlags.includes(serie.original_language)"
                                :src="getImagePath(serie.original_language)" alt="flags">
                            <span v-else>{{ serie.original_language }}</span>
                        </p>
                    </li>
                    <li>
                        <span>Voto: {{ serie.vote_average }}/10</span>
                    </li>
                </ul>
            </li>
        </ul>
    </main>
</template>

<style lang="scss" scoped>
img {
    width: 10px;
}
</style>