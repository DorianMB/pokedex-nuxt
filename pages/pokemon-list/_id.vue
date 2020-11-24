<template>
  <div>
    <h1>{{ pokemon.name }} </h1>
    <h2>{{ pokemon.weight }} - {{ pokemon.height }}</h2>
    <p 
      v-for="(type, index) in pokemon.types"
      :key="index"
      :type-data="type"
    >
      {{ type }} 
    </p>
    <p> Taille : {{ pokemon.height }} cm - Poids : {{ pokemon.weight }} kg </p>
  </div>
</template>

<script>
export default {
  name: "pokemon_id",
  async asyncData({ params }) {
    const id = params.id;
    return { id }
  },
  data(){
    return {
      pokemon: []
      }
  },
  mounted(){
    this.getPokemon();
  },
  methods: {
    async getPokemon(){
      const res = await this.$axios.$get('https://pokeapi.co/api/v2/pokemon/'+this.id)
      this.pokemon = res
      this.pokemon.weight = res.weight/10
      this.pokemon.size = res.size/10
      this.pokemon.types = res.types.map(p => p.type.name)
    }
  }
}
</script>

<style scoped>

</style>
