<template>
    <div>{{ data }}</div>
</template>

<script lang="ts">

export default {
    name: "pokemon-list",
    data() { 
        return {
            data: []
        }
    },
    mounted() {
        this.fetchPokemonCollection()
    },
    methods: {
        async fetchPokemonCollection(){
            const res = await this.$axios.get('https://pokeapi.co/api/v2/pokemon?limit=100')
            const data = res.data
        }
    }
}

</script>

<style lang="scss">
</style>