<template>
    <div class="logo">
        <a href="#" @click="sendRequest">
            <img src="@/assets/img/Netflix-logo.png" alt="Logo Netflix">
        </a>
    </div>
</template>

<script>
import axios from "axios";
import state from "@/state";
export default {
    name: 'LogoComponent',
    data() {
        return {
            query: 'one piece',
            API_FILM: "https://api.themoviedb.org/3/search/movie?api_key=702310bcccbb65c268d940c10a9c9146&language=it-IT&page=1&include_adult=false&query=",
            API_SERIE: "https://api.themoviedb.org/3/search/tv?api_key=702310bcccbb65c268d940c10a9c9146&language=en-US&page=1&include_adult=false&query=",
        }
    },
    methods: {
        sendRequest() {
           
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
    }


}
</script>

<style lang="scss" scoped>
    .logo {
        width: 160px;
        img {
            max-width: 100%;
        }
    }

    @media screen and (max-width: 400px) {

    img {
        width: 100px;
    }
    
}
</style>