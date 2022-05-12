<template>
    <div class="jumbo_tron">
        <img class="h-100 w-100 img-fluid fade-in-out" :src="jumboImg[active].src" :alt="jumboImg[active].alt">
    </div>
</template>

<script>
export default {
    name: 'JumbotronComponent',
    data() {
        return {
            active: 0,
            jumboImg: [
                {
                    id: 1,
                    src: require("@/assets/img/jumbotron_1.jpg"),
                    alt: "Demon Slayer poster"
                },
                {
                    id: 2,
                    src: require("@/assets/img/jumbotron_2.jpg"),
                    alt: "Juijutsu Kaisen poster"
                },
                {
                    id: 3,
                    src: require("@/assets/img/jumbotron_3.jpg"),
                    alt: "Made in Abyss poster"
                },
                {
                    id: 4,
                    src: require("@/assets/img/jumbotron_4.jpg"),
                    alt: "My Hero Academia poster"
                },
                {
                    id: 5,
                    src: require("@/assets/img/jumbotron_5.jpg"),
                    alt: "Prossime uscite poster"
                },

            ]
        }
    },
    methods: {
        timer() {
            setInterval(() => {
                if (this.active === this.jumboImg.length - 1) {
                    this.active = 0
                } else {
                    this.active++
                }
            }, 5000);
        }
    },
    mounted() {
        this.timer()

    }
}
</script>

<style lang="scss" scoped>
.jumbo_tron {
    /* background-image: url(@/assets/img/jumbotron_3.jpg);
        background-repeat: no-repeat;
        background-position: top, center;
        background-size: cover; */
    width: 100%;
    height: 60vh;

    img {
        object-fit: cover;
        object-position: top center;
        box-shadow: 0px -20px 20px 19px #6f6483;
    }

    .fade-in-out {
        animation: fade 5s infinite;
    }

    @keyframes fade {
        0% {
            filter: blur(30px);
            opacity: 0.7;
        }

        15% {
            filter: blur(0px);
            opacity: 1;
        }

        90% {
            filter: blur(0px);
            opacity: 1;
        }

        100% {
            filter: blur(30px);
            opacity: 0.7;
        }

    }
}
</style>