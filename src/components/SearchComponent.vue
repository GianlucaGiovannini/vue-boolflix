<template>
    <div class="search_bar d-flex align-items-center">
        <input v-model="query" type="text" placeholder="Cerca un film" @keyup.enter="sendRequest">
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
            API_URL: "https://api.themoviedb.org/3/search/movie?api_key=702310bcccbb65c268d940c10a9c9146&language=it-IT&page=1&include_adult=false&query=",
            querySearch: [],
        }
    },
    methods: {
        sendRequest() {
            axios.get(`${this.API_URL}${this.query.toLowerCase()}`).then(response => {
            this.querySearch = response.data.results
            state.querySearch = this.querySearch
            })
            .catch(error => {
            console.log(error)
            })
        }
    }
}
</script>

<style lang="scss" scoped>

    input {
        width: 280px;
        padding: 0.2rem 0.65rem ;
    }
    .search_icon {
        color: white;
        font-size: 1.5rem;
        padding: 0 0.75rem;
        cursor: pointer;
    }
</style>