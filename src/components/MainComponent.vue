<template>
    <main>
        <JumboComponent />
        <div class="container-fluid px-5">
            <div
                class="row row-cols-1 row-cols-sm-2 row-cols-md-3 row-cols-lg-4 row-cols-xl-5 row-cols-xxl-6 py-5 px-4 px-md-5 g-4">
                <CardContainer :list="list" v-for="list in filteredSearch" :key="list.id" />

            </div>
        </div>
    </main>
</template> 
 
<script>
import state from "@/state";
import JumboComponent from "@/components/JumbotronComponent.vue"
import CardContainer from "@/components/CardContainerComponent.vue"



export default {
    name: 'MainComponent',
    components: {
        JumboComponent,
        CardContainer
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
        /* voteNumber(voto) {
            return Math.round(Number(voto) / 2)
        }, */
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


