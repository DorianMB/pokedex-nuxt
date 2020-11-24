<template>
  <div class="flex flex-col items-center mx-20">
    <Logo/>
    <div class="pokedex w-full h-64 rounded-2xl flex flex-col justify-center items-center">
      <p>Choisissez votre starter</p>
      <div class="flex justify-center items-center">
        <div v-for="(pokemon,index) in pokemons" :key="index" class="mx-8 flex flex-col items-center">
          <img :src="pokemon.sprites.front_default">
          <span>{{getPokemon(pokemon)}}</span>
        </div>
      </div>
    </div>
    <router-link to="pokemon-list" tag="button" class="bg-red-100 mt-5 rounded-full py-3 px-6 shadow flex justify-center items-center">
      <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor" class="w-6 mr-3">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2m-3 7h3m-3 4h3m-6-4h.01M9 16h.01" />
      </svg>
      <span>Go to list</span>
    </router-link>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
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
  },
  methods: {
    getPokemon(pokemon: any) {
      console.log(pokemon, 'abcd');
      return pokemon.name;
    }
  }
})
</script>

<style lang="scss">
  .pokedex {
    background-color: white;
    box-shadow: inset 0 2px 4px 0 rgba(0, 0, 0, 0.6);
  }
</style>
