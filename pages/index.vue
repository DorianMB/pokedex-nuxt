<template>
  <div class="flex flex-col items-center mx-20">
    <Logo/>
    <div class="pokedex w-full rounded-2xl flex flex-col justify-center items-center py-6">
      <p class="mb-6">Choisissez votre starter</p>
      <div class="flex justify-center items-center">
        <div v-for="(pokemon,index) in pokemons" :key="index" class="mx-8">
          <pokemon-card :pokemon="pokemon"></pokemon-card>
        </div>
      </div>
    </div>
    <router-link to="pokemon-list" tag="button" class="bg-white text-primary mt-5 rounded-full py-3 px-6 shadow flex justify-center items-center">
      <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor" class="w-6 mr-2">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2m-3 7h3m-3 4h3m-6-4h.01M9 16h.01" />
      </svg>
      <span>Go to list</span>
    </router-link>
  </div>
</template>

<script>
import Vue from 'vue'
import PokemonCard from "~/components/PokemonCard.vue";

export default Vue.extend({
  components: {PokemonCard},
  data() {
    return {
      pokemons: [null]
    }
  },
  beforeMount() {
    this.pokemons = [];
    this.$axios.$get('https://pokeapi.co/api/v2/pokemon/bulbasaur').then(res => {
      this.pokemons.push(res);
    });
    this.$axios.$get('https://pokeapi.co/api/v2/pokemon/squirtle').then(res => {
      this.pokemons.push(res);
    });
    this.$axios.$get('https://pokeapi.co/api/v2/pokemon/charmander').then(res => {
      this.pokemons.push(res);
    });
  }
})
</script>

<style lang="scss">
  .pokedex {
    background-color: white;
    box-shadow: inset 0 2px 4px 0 rgba(0, 0, 0, 0.6);
  }
</style>
