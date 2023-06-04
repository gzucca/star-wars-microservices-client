<template>
  <section tabindex="0" @keyup.esc="props.closePopup" class="card__background">
    <h1 class="card__title">{{ title }}</h1>
    <div class="card__list">
      <p class="card__item">Opening crawl: {{ opening_crawl }}</p>
      <p class="card__item">Director: {{ director }}</p>
      <p class="card__item">Producer: {{ producer }}</p>
      <p class="card__item">
        Release date: {{ release_date.split("T")[0] }}
      </p>
    </div>
    <div v-if="characters.length > 0">
      <h2 class="card__subtitle">Characters:</h2>
      <div class="card__list">
        <p v-for="character in characters" class="card__item">
          {{ character.name }}
        </p>
      </div>
    </div>
    <button class="card__button" @click="props.closePopup">CLOSE</button>
  </section>
</template>

<script setup>
  const props = defineProps([
    "_id",
    "title",
    "opening_crawl",
    "director",
    "producer",
    "release_date",
    "characters",
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
    position: absolute;
    top: 50%;
    left: 50%;
    -ms-transform: translate(-50%, -50%);
    transform: translate(-50%, -50%);
  }

  .card__title {
    font-size: x-large;
    margin-block: 1rem;
  }

  .card__list {
    display: flex;
    flex-wrap: wrap;
    gap: 1rem;
  }

  .card__item {
    font-weight: 500;
    font-size: large;
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
      font-size: larger;
    }
    .card__title {
      font-size: xx-large;
    }

    .card__subtitle {
      font-size: x-large;
    }
  }
</style>
