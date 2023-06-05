<template>
  <section tabindex="0" @keyup.esc="props.closePopup" class="card__background">
    <h1 class="card__title">{{ name }}</h1>
    <div class="card__list">
      <p class="card__item">Birth year: {{ birth_year }}</p>
      <p class="card__item">Eye color: {{ eye_color }}</p>
      <p class="card__item">Gender: {{ gender }}</p>
      <p class="card__item">Hair color: {{ hair_color }}</p>
      <p class="card__item">Height: {{ height }} cm</p>
      <p class="card__item">Mass: {{ mass }} kg</p>
      <p class="card__item">Skin Color: {{ skin_color }}</p>
      <p class="card__item">Homeworld: {{ homeworld.name }}</p>
    </div>
    <div v-if="films.length > 0">
      <h2 class="card__subtitle">Films</h2>
      <div class="card__list">
        <p v-for="film in films" class="card__item">{{ film.title }} -</p>
      </div>
    </div>
    <button class="card__button" @click="props.closePopup">CLOSE</button>
  </section>
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
    position: relative;
    height: fit-content;
    width: 60vw;
    border-radius: 10px;
    padding: 1rem;
    margin: 0;
    top: 50%;
    left: 50%;
    -ms-transform: translate(-50%, -50%);
    transform: translate(-50%, -50%);
    max-height: 100%;
    overflow-y: auto;
  }

  .card__title {
    font-size: x-large;
    margin-block: 1rem;
  }

  .card__list {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
  }

  .card__item {
    font-weight: 400;
    font-size: medium;
  }

  .card__subtitle {
    margin-block: 1rem;
    font-size: larger;
  }

  .card__button {
    color: #9effff;
    background: rgba(184, 237, 255, 0.1);
    border: solid 1px #9effff;
    border-radius: 5px;
    padding: 0.8em 1em;
    cursor: pointer;
    margin-block: 1rem;
    font-size: large;
    font-weight: 600;
  }

  @media screen and (min-width: 900px) {
    .card__button,
    .card__item {
      font-size: large;
    }
    .card__title {
      font-size: xx-large;
    }

    .card__subtitle {
      font-size: x-large;
    }
  }
</style>
