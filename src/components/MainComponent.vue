<template>
    <main>
        <div class="container-fluid">
            <div class="row row-cols-2 row-cols-md-3 row-cols-lg-4 row-cols-xl-5 row-cols-xxl-6  py-4 px-3 px-md-5 g-4">
                <div class="col" v-for="list in filteredSearch" :key="list.id">
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
                    <div class="list_language" v-else-if="list.original_language == 'ja'">
                    <flag iso="jp" />
                    </div>
                    <div class="list_language" v-else>
                        <flag :iso="list.original_language" />
                    </div>
                    <!-- <div class="stars d-flex gap-1">
                        <div class="list_vote me-2">Voto: {{voteNumber(list.vote_average)}}</div>
                        <div :class="list.vote_average >= 2 ? 'active_star' : ''"><font-awesome-icon icon="fa-solid fa-star" /></div>
                        <div :class="list.vote_average >= 4 ? 'active_star' : ''"><font-awesome-icon icon="fa-solid fa-star" /></div>
                        <div :class="list.vote_average >= 6 ? 'active_star' : ''"><font-awesome-icon icon="fa-solid fa-star" /></div>
                        <div :class="list.vote_average >= 8 ? 'active_star' : ''"><font-awesome-icon icon="fa-solid fa-star" /></div>
                        <div :class="list.vote_average >= 9 ? 'active_star' : ''"><font-awesome-icon icon="fa-solid fa-star" /></div>
                    </div> -->
                    <Rate class="viaSlot" :length="5" :value="voteNumber(list.vote_average)" :readonly="true">
                        <svg width="22" height="21" viewBox="0 0 20 19" fill="none" xmlns="http://www.w3.org/2000/svg">
                            <path
                            fill-rule="evenodd"
                            clip-rule="evenodd"
                            d="M12.034 7.074H19.416L13.445 11.448L15.726 18.524L9.75201 14.151L3.77901 18.524L6.06101 11.448L0.0880127 7.075H7.47001L9.75201 0.002V0L12.034 7.075V7.074Z"
                            fill="currentColor"/>
                        </svg>
                    </Rate>
                </div>
            </div>
        </div>
    </main> 
</template> 
 
<script>
import state from "@/state";
import Rate from '../../node_modules/vue-rate/src/Rate.vue';

export default {
    name: 'MainComponent',
    components: {
        Rate
    },
    props: {

    },
    data() { 
        return {
            listSeriesFilms: '' 
        }
    }, 
    methods: {
        changeList(){
            this.listSeriesFilms = state.querySearch
        },
        voteNumber(voto){
            return Math.round(Number(voto) / 2)
        }
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

<style lang="scss" scoped>

.row {
    /* .active_star {
    color: yellow;
    } */
}

</style>