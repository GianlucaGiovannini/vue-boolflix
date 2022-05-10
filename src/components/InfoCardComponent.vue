<template>
    <div class="card_info">
        <div href="#" class="details_actor fs-6 d-flex justify-content-end"
            :class="infoDetails ? 'details_active' : 'details_not_active'" @click="infoDetailsKey">
            <font-awesome-icon icon="fa-solid fa-circle-info" />
        </div>
        <div v-if="!infoDetails" class="info_card h-100 d-flex flex-column justify-content-between">
            <div class="card_title">
                <div class="list_title" v-if="list.title">
                    <div class="fw_bold">Titolo:</div> {{ list.title }}
                </div>
                <div class="list_name" v-else>
                    <div class="fw_bold">Titolo:</div> {{ list.name }}
                </div>
            </div>
            <div class="card_release">
                <div class="list_release" v-if="list.release_date == '' || !list.release_date">
                    <div class="fw_bold">Data di uscità</div> Sconosciuta
                </div>
                <div class="list_release" v-else>
                    <div class="fw_bold">Data di uscità</div> {{ list.release_date }}
                </div>
            </div>
            <div class="card_lenguage">
                <div class="list_language fw_bold d-flex align-items-center gap-2"
                    v-if="list.original_language == 'en'">
                    Lingua originale:
                    <span class="fs-6">
                        <flag iso="gb" />
                    </span>
                </div>
                <div class="list_language fw_bold d-flex align-items-center gap-2"
                    v-else-if="list.original_language == 'ja'">
                    Lingua originale:
                    <span class="fs-6">
                        <flag iso="jp" />
                    </span>
                </div>
                <div class="list_language fw_bold d-flex align-items-center gap-2" v-else>
                    Lingua originale:
                    <span class="fs-6">
                        <flag :iso="list.original_language" />
                    </span>
                </div>
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
        <div v-else class="info_cast h-100 d-flex flex-column justify-content-between">
            <div class="cast" v-for="cast in detailsExtract" :key="cast.cast_id">
                {{ cast.character }}
                <div>
                    <span class="fw_bold">Interprete:</span> {{ cast.name }}
                </div>
            </div>
        </div>

    </div>
</template>

<script>
import axios from "axios"

export default {
    name: 'InfoCardComponent',
    props: {
        list: Object,
    },
    data() {
        return {
            infoDetails: false,
            idExtract: '',
            detailsExtract: [],
        }

    },
    methods: {
        infoDetailsKey() {
            if (!this.infoDetails) {
                this.infoDetails = true
                this.idExtract = this.list.id
                this.requestDetails()
            } else {
                this.infoDetails = false
            }
        },

        clearDetails() {
            /* console.log(this.detailsExtract) */
            this.detailsExtract.splice(0, this.detailsExtract)
        },

        requestDetails() {
            this.clearDetails()
            
            if (this.list.name == null) {
                axios.get(`https://api.themoviedb.org/3/movie/${this.idExtract}/credits?api_key=702310bcccbb65c268d940c10a9c9146`).then(response => {
                    const result = response.data.cast
                    result.forEach(element => {
                        if (this.detailsExtract.length <= 3) {
                            this.detailsExtract.push(element)
                        }
                    });
                })
                    .catch(error => {
                        console.log(error)
                    });
                this.idExtract = ''
            } else {
                axios.get(`https://api.themoviedb.org/3/tv/${this.idExtract}/credits?api_key=702310bcccbb65c268d940c10a9c9146`).then(response => {
                    const result = response.data.cast
                    result.forEach(element => {
                        if (this.detailsExtract.length <= 3) {
                            this.detailsExtract.push(element)
                        }
                    });
                })
                    .catch(error => {
                        console.log(error)
                    });
                this.idExtract = ''
            }

        }
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

    .details_actor {
        cursor: pointer;
    }

    .details_active {
        color: #3a79b7;
    }

    .details_not_active {
        color: white;
    }

    .stars {
        font-size: 0.9rem;

        .active_star {
            color: yellow;
        }
    }

    .cast {
        font-size: 0.6rem;

        div {
            font-size: 0.5rem;

        }

    }

    .fw_bold {
        font-weight: 700;
        color: #c2baba;
    }

}
</style>
