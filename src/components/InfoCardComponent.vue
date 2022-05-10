<template>
    <div class="card_info">
        <div class="list_title" v-if="list.title">
            <div class="fw-bold">Titolo:</div> {{ list.title }}
        </div>
        <div class="list_name" v-else>
            <div class="fw-bold">Titolo:</div> {{ list.name }}
        </div>
        <div class="list_release" v-if="list.release_date == '' || !list.release_date">
            <div class="fw-bold">Data di uscità</div> Sconosciuta
        </div>
        <div class="list_release" v-else>
            <div class="fw-bold">Data di uscità</div> {{ list.release_date }}
        </div>
        <div class="list_language fw-bold d-flex align-items-center gap-2" v-if="list.original_language == 'en'">
            Lingua originale:
            <span class="fs-6">
                <flag iso="gb" />
            </span>
        </div>
        <div class="list_language fw-bold d-flex align-items-center gap-2" v-else-if="list.original_language == 'ja'">
            Lingua originale:
            <span class="fs-6">
                <flag iso="jp" />
            </span>
        </div>
        <div class="list_language fw-bold d-flex align-items-center gap-2" v-else>
            Lingua originale:
            <span class="fs-6">
                <flag :iso="list.original_language" />
            </span>
        </div>
        <div class="stars d-flex gap-1">
            <!-- <div class="list_vote me-2">Voto: {{ voteNumber(list.vote_average) }}</div> -->
            <div :class="list.vote_average >= 2 ? 'active_star' : ''">
                <font-awesome-icon icon="fa-solid fa-star" />
            </div>
            <div :class="list.vote_average >= 4 ? 'active_star' : ''">
                <font-awesome-icon icon="fa-solid fa-star" />
            </div>
            <div :class="list.vote_average >= 6 ? 'active_star' : ''">
                <font-awesome-icon icon="fa-solid fa-star" />
            </div>
            <div :class="list.vote_average >= 8 ? 'active_star' : ''">
                <font-awesome-icon icon="fa-solid fa-star" />
            </div>
            <div :class="list.vote_average >= 9 ? 'active_star' : ''">
                <font-awesome-icon icon="fa-solid fa-star" />
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'InfoCardComponent',
    props: {
        list: Object,
    }
}
</script>

<style lang="scss">
.card_info {
    display: none;
    font-size: 0.65rem;
    width: 100%;
    height: 65%;
    padding: 1rem 0.5rem;
    color: white;
    background-color: rgba(0, 0, 0, 0.904);
    position: absolute;
    left: 0;
    bottom: -13%;

    .stars {
        font-size: 0.9rem;

        .active_star {
            color: yellow;
        }
    }
}
</style>
