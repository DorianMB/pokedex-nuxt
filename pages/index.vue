<template>
  <div class="flex flex-col items-center">
    <Logo />
    <div class="pokedex w-full h-64 rounded">
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  beforeMount(): void {
    //this.asyncData();
  },
  methods: {
    async asyncData() {
      const ip = await this.$axios.$get('http://icanhazip.com');
      console.log(ip, 'abcd');
      return { ip }
    }
  }
})
</script>

<style lang="scss">
  .pokedex {
    background-color: white;
    box-shadow: inset 0 2px 4px 0 rgba(0, 0, 0, 0.6);
    margin: 1rem 5rem;
  }
</style>
