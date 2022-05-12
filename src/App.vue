<template>
  <div id="app">
    <div class="entrance d-flex justify-content-center align-items-center min-vw-100 min-vh-100" v-if="entranceKey">
      <div class="logo_container">
        <LogoComponent />
      </div>
    </div>

    <div class="site" v-else>
      <SiteHeader />
      <SiteMain />
    </div>



  </div>
</template>

<script>
import SiteHeader from "@/components/HeaderComponent.vue"
import SiteMain from "@/components/MainComponent.vue"
import LogoComponent from "./components/LogoComponent.vue"

export default {
  name: 'App',
  components: {
    SiteHeader,
    SiteMain,
    LogoComponent
  },
  data() {
    return {
      entranceKey: true
    }
  },
  methods: {
    timerEntrance() {
      setTimeout(() => {
        this.entranceKey = false
      }, 1200);
    }
  },
  mounted(){
    this.timerEntrance()
  }
}
</script>

<style lang="scss">
@import "@/assets/scss/style.scss";

.logo_container {
  animation: entrance 3s;
}

@keyframes entrance {
  0% {
    transform: scale(1);
  }

  100% {
    transform: scale(7);
  }
}
</style>
