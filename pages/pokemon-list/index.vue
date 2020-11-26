<template>
  <div class="flex flex-col items-center mx-20 pb-3">
    <Logo/>
    <div class="pokedex w-full rounded-2xl grid grid-cols-3 gap-4 py-6" v-if="pokemons.length > 0">
      <div v-for="(pokemon,index) in pokemons" :key="index" class="mx-8 flex justify-center">
        <pokemon-card :pokemon="getPokemonInfos(pokemon.url)"></pokemon-card>
      </div>
    </div>
  </div>
</template>

<script>
import PokemonCard from "../../components/PokemonCard";
export default {
  name: "index.vue",
  components: {PokemonCard},
  data(){
    return {
      pokemons: []
    }
  },
  beforeMount() {
    this.getPokemon();
  },
  methods: {
    async getPokemon() {
      this.$axios.$get('https://pokeapi.co/api/v2/pokemon?limit=151').then(res => {
        this.pokemons = res['results'];
      })
    },
    async getPokemonInfos(url) {
      return await this.$axios.$get(url);
    }
  }
}
</script>

<style lang="scss"  scoped>
  .pokedex {
    background-color: white;
    box-shadow: inset 0 2px 4px 0 rgba(0, 0, 0, 0.6);
  }
</style>

