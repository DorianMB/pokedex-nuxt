<template>
  <div>
    <pokemon-card
      v-for="(pokemon, index) in pokemons"
      :key="index"
      :pokemon="pokemon"
    />
  </div>
</template>

<script>
export default {
  name: "index.vue",
  data(){
    return {
      pokemons: []
    }
  },
  mounted() {
    this.getPokemonList();
  },
  methods: {
    async getPokemonList() {
      const res = await this.$axios.$get('https://pokeapi.co/api/v2/pokemon?limit=60')
      this.pokemons = res['results']
    }
  }
}
</script>

<style scoped>

</style>

