<template>
    <main>
        <div class="films" v-for="film in films" :key="film.id"></div>
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

    mounted(){
        console.log(state)
    }
}

</script>

<style>

</style>