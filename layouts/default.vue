<template>
  <div class="container">
    <Nuxt/>
  </div>
</template>


<script>
export default {
  methods: {
  },
  created(context) {
    this.$pouch.sync('participants', 'https://testcouch.ecsplico.de/participants');
  }
}
</script>
<style scoped>
.container {
  margin: 12px;
}
</style>
