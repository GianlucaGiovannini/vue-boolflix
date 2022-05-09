<template>
    <main>
        <div class="container-fluid">
            <div class="row row-cols-2 row-cols-md-3 row-cols-lg-4 row-cols-xl-5 row-cols-xxl-6 px-6 gap-4 justify-content-center">
                <div class="col " v-for="list in filteredSearch" :key="list.id">
                    <div class="list_img">
                        <img :src="'https://image.tmdb.org/t/p/w342'+list.poster_path">
                    </div>
                    <div class="list_title" v-if="list.title">{{list.title}}</div>
                    <div class="list_name" v-else>{{list.name}}</div>
                    <div class="list_original_title" v-if="list.original_title">{{list.original_title}}</div>
                    <div class="list_original_name" v-else>{{list.original_name}}</div>
                    <div class="list_language" v-if="list.original_language == 'en'">
                    <flag iso="gb" />
                    </div>
                    <div class="list_language" v-if="list.original_language == 'ja'">
                    <flag iso="jp" />
                    </div>
                    <div class="list_language" v-else>
                        <flag :iso="list.original_language" />
                    </div>
                    <div class="stars d-flex gap-1">
                        <div class="list_vote me-2">Voto: {{list.vote_average}}</div>
                        <div :class="list.vote_average >= 2 ? 'active_star' : ''"><font-awesome-icon icon="fa-solid fa-star" /></div>
                        <div :class="list.vote_average >= 4 ? 'active_star' : ''"><font-awesome-icon icon="fa-solid fa-star" /></div>
                        <div :class="list.vote_average >= 6 ? 'active_star' : ''"><font-awesome-icon icon="fa-solid fa-star" /></div>
                        <div :class="list.vote_average >= 8 ? 'active_star' : ''"><font-awesome-icon icon="fa-solid fa-star" /></div>
                        <div :class="list.vote_average >= 9 ? 'active_star' : ''"><font-awesome-icon icon="fa-solid fa-star" /></div>
                    </div>


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
            listSeriesFilms: '' 
        }
    }, 
    methods: {
        changeList(){
            this.listSeriesFilms = state.querySearch
        },
    },
    computed: {
        filteredSearch(){
            this.changeList()
            return this.listSeriesFilms.filter(film => {
            if(film.poster_path != null) {
                return film
                }
            })
        },

    }
}
</script>

<style>
.active_star {
    color: yellow;
}
</style>