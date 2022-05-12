<template>
    <header :class="scrollHeader >= 90 ? 'scroll_y' : '' ">
        <div class="container-fluid">
            <nav class="d-flex justify-content-between align-items-center px-1 px-md-3">
                <LogoComponent />
                <SearchComponent />
            </nav>
        </div>
    </header>
</template>

<script>
import LogoComponent from '@/components/LogoComponent.vue'
import SearchComponent from '@/components/SearchComponent.vue'
export default {
    name: 'HeaderComponent',
    data() {
        return {
            scrollHeader: '',
        }
    },
    components: {
        LogoComponent,
        SearchComponent
    },
    methods: {
        
    },
    mounted(){
        window.addEventListener("scroll", () => {
            this.scrollHeader = window.scrollY
            /* console.log(window.scrollY)
            console.log(this.scrollHeader) */
        });
    }
}
</script>

<style lang="scss" scoped>
header {
    width: 100%;
    height: 90px;
    background-color: transparent;
    position: fixed;
    top: 0;
    left: 0;
    z-index: 3;
    transition: background-color 1.3s;

    nav {
        height: 90px;
    }
    &:hover {
        background-color: rgb(20 20 20 / 95%); 
    }
}

.scroll_y {
        background-color: rgb(20 20 20 / 95%);        
    }


</style>