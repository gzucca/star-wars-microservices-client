<template>
  <div tabindex="0" @keyup.esc="props.closePopup" class="card__background">
    <h1 class="card__title">{{ props.name }}</h1>
    <button class="card__button" @click="props.closePopup">CLOSE</button>
  </div>
</template>

<script setup>
  const props = defineProps([
    "birth_year",
    "eye_color",
    "films",
    "gender",
    "hair_color",
    "height",
    "homeworld",
    "mass",
    "name",
    "skin_color",
    "_id",
    "closePopup",
  ]);
</script>

<style scoped>
  .card__background {
    background: rgba(184, 237, 255, 0.1);
    color: #9effff;
    border: solid 3px rgba(127, 222, 254, 0.4);
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    margin: auto;
    height: 70vh;
    width: 60vw;
    border-radius: 10px;
  }

  .card__title {
    margin: 0;
  }

  .card__button {
    color: #9effff;
    background: rgba(184, 237, 255, 0.1);
    border: solid 1px #9effff;
    border-radius: 5px;
    padding: 0.8em 1em;
    cursor: pointer;
  }

  @media screen and (min-width: 900px) {
  }
</style>
