<template>
    <div class="search_bar d-flex align-items-center">
        <input type="text" placeholder="Cerca un film">
        <div class="search_icon">
            <font-awesome-icon icon="fa-solid fa-magnifying-glass" />
        </div>
        
    </div>
</template>

<script>
export default {
    name: 'SearchComponent'
}
</script>

<style lang="scss" scoped>

    input {
        width: 280px;
    }
    .search_icon {
        font-size: 1.5rem;
        padding: 0 0.5rem;
    }
</style>