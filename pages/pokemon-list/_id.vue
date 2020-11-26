<template>
  <div class="px-6 flex flex-col items-center min-h-screen">
    <Logo/>
    <div class="pokedex w-full rounded-2xl flex items-center p-6" v-if="pokemon.id">
      <div class="rounded-xl w-2/6 flex flex-col items-center pokemon-card shadow">
        <div class="w-full bg-black text-white px-4 py-1 pokemon-header flex justify-between">
          <div class="flex items-center">
            <img src="../../assets/images/pokeball.png" class="w-10 mr-2">
            <span>N°{{pokemonNumber}}</span>
          </div>
          <span>{{pokemon.name | capitalize}}</span>
        </div>
        <img :src="pokemon.sprites.front_default" class="w-2/3">
      </div>

      <div class="pokemon-info flex flex-wrap h-full w-4/6 px-8">
        <div class="w-1/2">
          Type
        </div>
        <div class="w-1/2">
          <span
            v-for="(type, index) in pokemon.types"
            :key="index"
            :type-data="type"
            class="badge rounded mx-1 px-3"
          >
            {{ type }}
          </span>
        </div>
        <div class="w-1/2">Taille</div>
        <div class="w-1/2">{{ pokemon.height }} m </div>
        <div class="w-1/2">Poids</div>
        <div class="w-1/2">{{ pokemon.weight }} kg </div>
      </div>

    </div>
    <router-link to="/pokemon-list" tag="button" class="bg-white text-primary mt-5 rounded-full py-3 px-6 shadow flex justify-center items-center">
      <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor" class="w-6 mr-2">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2m-3 7h3m-3 4h3m-6-4h.01M9 16h.01" />
      </svg>
      <span>Go to list</span>
    </router-link>
  </div>
</template>

<script>
import PokemonCard from "../../components/PokemonCard";

export default {
  name: "pokemon_id",
  components: {PokemonCard},
  async asyncData({params}) {
    const id = params.id;
    return {id}
  },
  data() {
    return {
      pokemon: []
    }
  },
  computed:{
    pokemonNumber() {
      if (this.pokemon.id) {
        let res = this.pokemon.id.toString();
        while (res.length < 4) {
          res = '0' + res;
        }
        return res;
      } else {
        return '';
      }
    }
  },
  beforeMount() {
    this.getPokemon();
  },
  methods: {
    async getPokemon() {
      this.$axios.$get('https://pokeapi.co/api/v2/pokemon/' + this.id).then(res => {
        console.log('abcd', res);
        this.pokemon = res;
        this.pokemon.weight = res.weight / 10;
        this.pokemon.height = res.height / 10;
        this.pokemon.types = res.types.map(p => p.type.name);
      });
    },
  },
  filters: {
    capitalize: function (value) {
      if (!value) return '';
      value = value.toString();
      return value.charAt(0).toUpperCase() + value.slice(1);
    }
  }
}
</script>

<style scoped lang="scss">
  .pokedex {
    background-color: white;
    box-shadow: inset 0 2px 4px 0 rgba(0, 0, 0, 0.6);
  }

  .pokemon-card {
    img {
      background-image: url("../../assets/images/pokeball-bg.png");
      background-repeat: no-repeat;
      background-size: 16rem;
      background-position: center;
    }

    background-color: rgba(255, 255, 255, 0.05);

    .pokemon-header {
      border-radius: 10px 10px 0 0;
      background-color: rgba(27, 94, 171, 0.85);
      font-size: 24px;
    }
  }

  .pokemon-info {
    div {
      border: 1px solid #e2e8f0;
      height: 56px;
      display: flex;
      align-items: center;
      padding: 0 1.5rem;
      .badge {
        border: 1px solid #e2e8f0;
        font-size: 12px;
      }
    }
  }
</style>
