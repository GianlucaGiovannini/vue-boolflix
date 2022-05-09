<template>
    <header>
        <div class="container-fluid">
            <nav class="d-flex justify-content-between align-items-center">
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
    padding: 1rem 1.5rem;
}
</style>