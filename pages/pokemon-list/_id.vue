<template>
  <div class="px-6 flex items-center min-h-screen">
    <div class="pokedex w-full rounded-2xl flex items-center p-6" v-if="pokemon.id">
      <div class="rounded-xl w-2/6 flex flex-col items-center pokemon-card shadow">
        <div class="w-full bg-black text-white px-4 py-1 pokemon-header flex justify-between">
          <div class="flex items-center">
            <img src="../../assets/images/pokeball.png" class="w-10 mr-2">
            <span>N°{{pokemonNumber(pokemon.id)}}</span>
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
  </div>
</template>

<script>
export default {
  name: "pokemon_id",
  async asyncData({params}) {
    const id = params.id;
    return {id}
  },
  data() {
    return {
      pokemon: []
    }
  },
  mounted() {
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
    pokemonNumber(id) {
      if (id) {
        let res = id.toString();
        while (res.length < 4) {
          res = '0' + res;
        }
        return res;
      } else {
        return '';
      }
    }
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

<style lang="scss">
  .pokedex {
    background-color: white;
    box-shadow: inset 0 2px 4px 0 rgba(0, 0, 0, 0.6);
  }

  .pokemon-card {
    img {
      background-image: url("../../assets/images/pokeball-bg.png");
      background-repeat: no-repeat;
      background-size: 12rem;
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
