<template>
    <main>
        <div class="container-fluid px-5">
            <div
                class="row row-cols-1 row-cols-sm-2 row-cols-md-3 row-cols-lg-4 row-cols-xl-5 row-cols-xxl-6 py-5 px-4 px-md-5 g-4">
                <div class="col" v-for="list in filteredSearch" :key="list.id">
                    <div class="card_container h-100">
                        <div class="list_img">
                            <img class="card_img" :src="'https://image.tmdb.org/t/p/w342' + list.poster_path">
                        </div>
                        <InfoCard :list="list" />
                    </div>
                </div>
            </div>
        </div>
    </main>
</template> 
 
<script>
import state from "@/state";
import InfoCard from "@/components/InfoCardComponent.vue"


export default {
    name: 'MainComponent',
    components: {
        InfoCard
    },
    data() {
        return {
            listSeriesFilms: '',
        }
    },
    methods: {
        changeList() {
            this.listSeriesFilms = state.querySearch
        },
        voteNumber(voto) {
            return Math.round(Number(voto) / 2)
        },
    },
    computed: {
        filteredSearch() {
            this.changeList()
            return this.listSeriesFilms.filter(film => {
                if (film.poster_path != null) {
                    return film
                }
            })
        },

    }
}
</script>

<style lang="scss">
.row {
    .col {
        height: 350px;
        overflow: hidden;
        transition-duration: 1s;

        img.card_img {
            height: 350px;
            width: 100%;
            object-fit: cover;
        }

        &:hover {
            padding: 2rem;
            transform: scale(1.7);
            z-index: 1;
            transition-delay: 0.7s;

            .card_info {
                display: flex;
                flex-direction: column;
                justify-content: space-between;
                box-shadow: inset 0px -10px 7px 0px #000000;
            }
        }
    }

    .card_container {
        position: relative;
    }
}
</style>