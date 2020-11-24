<template>
  <p>TG</p>
</template>

<script>
export default {
  name: "pokemon-list",
  mounted() {
    this.getPokemon();
  },
  methods: {
    async getPokemon() {
      const ip = await this.$axios.$get('http://icanhazip.com');
      console.log(ip, 'abcd');
      return { ip }
    }
  }
}
</script>

<style scoped>

</style>
