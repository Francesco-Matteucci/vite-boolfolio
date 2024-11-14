<script>
  export default {
    name: 'App',
    data() {
      return {
        message: 'Progetto Portfolio con vue',
      };
    },
    methods: {
      greet() {
        alert(this.message);
      },
    },
  };
</script>

<template>
  <div class="container mt-5">
    <h1 class="text-center">Vue 3 Boolfolio</h1>
    <p class="text-center">Progetto configurato con Bootstrap e Vue Option API</p>
  </div>
</template>

<style scoped></style>
