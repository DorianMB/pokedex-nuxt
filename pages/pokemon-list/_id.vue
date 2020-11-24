<template>
  <div>
    <h1>Details</h1>
    <h2>{{ id }}</h2>
  </div>
</template>

<script>
export default {
  name: "_id",
  beforeMount() {
    console.log('abcd', this.id);
  },
  async asyncData({ params }) {
    const id = params.id;
    return { id }
  },
}
</script>

<style scoped>

</style>
