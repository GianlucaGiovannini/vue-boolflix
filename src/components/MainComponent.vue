<template>
    <main>
        <div class="container-fluid">
            <div class="row row-cols-2 row-cols-md-3 row-cols-lg-4 row-cols-xl-5 row-cols-xxl-6 px-6 gap-4 justify-content-center">
                <div class="col " v-for="film in filteredFilms" :key="film.id">
                    <div class="film_img">
                        <img :src="'https://image.tmdb.org/t/p/w342'+film.poster_path" alt="">
                    </div>
                    <div class="film_title">{{film.title}}</div>
                    <div class="film_original_title">{{film.original_title}}</div>
                    <div class="film_language">
                        <flag iso="it" />
                    </div>
                    <div class="film_vote">{{film.vote_average}}</div>
                </div>
            </div>
        </div>
    </main>
</template>
 
<script>
import state from "@/state";
export default {
    name: 'MainComponent',
    data() {
        return {
            films: state.querySearch
        }
    },

    methods: {
        changeFilm(){
            this.films = state.querySearch
        }
    },
 
    computed: {
        filteredFilms(){
            return this.films.filter(film => {
                if(film.poster_path != null) {
                    return film
                }
            })
        } 
    }
}
</script>

<style>

</style>