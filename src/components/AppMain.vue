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
        },

        getNewRating(old_rating) {
            old_rating = old_rating / 2;
            return old_rating;
        }
    }

}
</script>

<template>
    <main>
        <ul>
            <li>
                <h2>MOVIES</h2>
            </li>
            <li class="element" v-for="movie in store.moviesList">
                <ul>
                    <li>
                        <img :src="`https://image.tmdb.org/t/p/w92${movie.poster_path}`" alt="">
                    </li>
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
                        Vote: <span v-for="n in 5"
                            :class="(n <= getNewRating(movie.vote_average)) ? 'full-star' : 'empty - star'">*</span>
                    </li>
                </ul>
                <hr>
            </li>
            <li>
                <h2>SERIES</h2>
            </li>
            <li class="element" v-for="serie in store.seriesList">
                <ul>
                    <li>
                        <img :src="`https://image.tmdb.org/t/p/w92${serie.poster_path}`" alt="">
                    </li>
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
p img {
    width: 10px;
}

h2 {
    margin-top: 2rem;
}

li.element {
    margin-top: 2rem;
}

hr {
    margin-top: 2rem;
}

.full-star {
    color: gold;
}

.empty-star {
    color: gray;
}
</style>