<template>
  <div class="stars d-flex gap-1">
                <!-- <div class="list_vote me-2">Voto: {{ voteNumber(list.vote_average) }}</div> -->
                <div :class="vote >= 2 ? 'active_star' : ''">
                    <font-awesome-icon icon="fa-solid fa-star" />
                </div>
                <div :class="vote >= 4 ? 'active_star' : ''">
                    <font-awesome-icon icon="fa-solid fa-star" />
                </div>
                <div :class="vote >= 6 ? 'active_star' : ''">
                    <font-awesome-icon icon="fa-solid fa-star" />
                </div>
                <div :class="vote >= 8 ? 'active_star' : ''">
                    <font-awesome-icon icon="fa-solid fa-star" />
                </div>
                <div :class="vote >= 9 ? 'active_star' : ''">
                    <font-awesome-icon icon="fa-solid fa-star" />
                </div>
            </div>
</template>

<script>
export default {
    name: 'StarVoteComponent',
    props: {
        vote: Number,
    }
}
</script>

<style lang="scss" scoped>
.stars {
        font-size: 0.9rem;

        .active_star {
            color: yellow;
        }
    }

</style>