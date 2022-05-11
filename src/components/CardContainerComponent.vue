<template>
    <div class="col">
        <div class="card_container h-100">
            <div class="list_img">
                <img class="card_img" :src="'https://image.tmdb.org/t/p/w342' + list.poster_path">
            </div>
            <InfoCard :list="list" />
        </div>
    </div>
</template>

<script>

import InfoCard from "@/components/InfoCardComponent.vue"

export default {
    name: 'CardContainerComponent',
    components: {
        InfoCard,
    },
    props: {
        list: Object
    }

}
</script>

<style lang="scss">
.row {
    margin-top: -8rem !important;

    .col {
        height: 350px;
        overflow: hidden;
        transition-duration: 1s;

        img.card_img {
            height: 350px;
            width: 100%;
            object-fit: cover;
            border-top-left-radius: 1.2rem;
            border-top-right-radius: 1.2rem;
            border-bottom-left-radius: 0.8rem;
            border-bottom-right-radius: 0.8rem;
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