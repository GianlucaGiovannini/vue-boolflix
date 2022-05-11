<template>
    <header>
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
    components: {
        LogoComponent,
        SearchComponent
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
    transition: background-color 2s;
    

    &:hover {
        background-color: rgb(20 20 20 / 93%);        
    }
}


</style>