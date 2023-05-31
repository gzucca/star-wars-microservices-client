<template>
  <div class="card__background">Hello!</div>
  <div>{{ characters }}</div>
</template>

<script setup>
  defineProps(["characters"]);

</script>

<style scoped>
  .card__background {
    background-color: rgba(184, 237, 255, 0.1);
    height: 100%;
    width: 100%;
    margin: 0;
    padding: 0;
    color: #9effff;
    border: 0;
  }

  @media screen and (min-width: 900px) {
  }
</style>
