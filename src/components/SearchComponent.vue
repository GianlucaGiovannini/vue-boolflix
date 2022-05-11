<template>
    <div class="search_bar d-flex align-items-center justify-content-end">
        <input v-model="query" type="text" placeholder="Search" @keyup.enter="sendRequest">
        <div class="search_icon">
            <font-awesome-icon icon="fa-solid fa-magnifying-glass" @click="sendRequest"/>
        </div>
        
    </div>
</template>

<script>
import axios from "axios"
import state from "@/state"
export default {
    name: 'SearchComponent',
    data() {
        return {
            query: '',
            API_FILM: "https://api.themoviedb.org/3/search/movie?api_key=702310bcccbb65c268d940c10a9c9146&language=it-IT&page=1&include_adult=false&query=",
            API_SERIE: "https://api.themoviedb.org/3/search/tv?api_key=702310bcccbb65c268d940c10a9c9146&language=en-US&page=1&include_adult=false&query=",
        }
    },
    methods: {
        sendRequest() {
            /* axios.get(`${this.API_FILM}${this.query.toLowerCase()}`).then(response => {
            state.querySearch = response.data.results
            console.log(state.querySearch)
            })
            .catch(error => {
            console.log(error)
            });

            axios.get(`${this.API_SERIE}${this.query.toLowerCase()}`).then(response => {
            state.querySearch = [...state.querySearch, ...response.data.results]
            console.log(state.querySearch)
            })
            .catch(error => {
            console.log(error)
            }); */

            let films = `${this.API_FILM}${this.query.toLowerCase()}`
            let series = `${this.API_SERIE}${this.query.toLowerCase()}`

            const requestFilm = axios.get(films)
            const requestSerie = axios.get(series)

            axios
            .all([requestFilm, requestSerie])
            .then(responses => {
            const responseOne = responses[0].data.results
            const responseTwo = responses[1].data.results

            state.querySearch = [...responseOne, ...responseTwo]
            })
            .catch(error => {
            console.log(error)
            })
            this.query = ''

        }
    },
    mounted() {
        this.query = "batman"
        this.sendRequest()

    }
}
</script>

<style lang="scss" scoped>

    input {
        width: 40%;
        padding: 0.2rem 0.65rem ;
        transition: width 1.5s;

        &:focus {
            width: 100%;
        }
        &:hover {
            width: 100%;
        }
    }
    .search_icon {
        color: white;
        font-size: 1.5rem;
        padding: 0 0.75rem;
        cursor: pointer;
    }
</style>