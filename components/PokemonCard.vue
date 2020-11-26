<template>
  <router-link v-if="pokemonData.id" tag="button" :to="'/pokemon-list/' + pokemonData.id"
               class="rounded-xl w-40 flex flex-col items-center pokemon-card shadow">
    <div class="w-full bg-black text-white text-left pl-2 py-1 pokemon-number flex">
      <img src="../assets/images/pokeball.png" class="w-6 mr-2">
      <span>N°{{pokemonNumber}}</span>
    </div>
    <img :src="pokemonData.sprites.front_default" class="w-40">
  </router-link>
</template>

<script>

export default {
  name: "pokemon-card",
  props: ['pokemon'],
  data() {
    return {
      pokemonData: {},
    }
  },
  computed:{
    pokemonNumber() {
      if (this.pokemonData.id) {
        let res = this.pokemonData.id.toString();
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
    if (this.pokemon && this.pokemon.id === undefined) {
      this.pokemon.then(res => {
        this.pokemonData = res;
      })
    } else {
      this.pokemonData = this.pokemon;
    }
  }
}

</script>

<style scoped lang="scss">
  .pokemon-card {
    img {
      background-image: url("../assets/images/pokeball-bg.png");
      background-repeat: no-repeat;
      background-size: 8rem;
      background-position: center;
    }

    background-color: rgba(255, 255, 255, 0.05);

    .pokemon-number {
      border-radius: 10px 10px 0 0;
      background-color: rgba(27, 94, 171, 0.85);
    }
  }
</style>
