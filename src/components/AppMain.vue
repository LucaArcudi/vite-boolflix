<script>
import { store } from "../store"

export default {
    name: "AppMain",
    data() {
        return {
            store,
        }
    },
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
                        <span>Lingua: {{ movie.original_language }}</span>
                    </li>
                    <li>
                        <span>Voto: {{ movie.vote_average }}/10</span>
                    </li>
                </ul>
            </li>
        </ul>
    </main>
</template>

<style lang="scss" scoped>

</style>