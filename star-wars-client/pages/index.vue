<template>
  <div v-if="state.showCharacter" class="home__card">
    <CharacterCard v-bind="state.character" :closePopup="closePopup" />
  </div>
  <div v-if="state.showFilm" class="home__card">
    <FilmCard v-bind="state.film" :closePopup="closePopup" />
  </div>
  <div v-if="state.showPlanet" class="home__card">
    <PlanetCard v-bind="state.planet" :closePopup="closePopup" />
  </div>

  <div class="home">
    <div class="home__scroll">
      <header class="container">
        <h1 class="home__title">Star Wars Microservices</h1>
      </header>
      <main class="container home__body">
        <section class="home__col">
          <h2 class="home__col__title">Characters</h2>
          <div class="home__col__list">
            <div v-bind="characters" v-for="character in characters">
              <h3
                tabindex="0"
                @keyup.esc="closePopup"
                @click="(event) => handleClickCharacter(event)"
                :_id="character._id"
                class="home__col__item"
              >
                {{ character.name }}
              </h3>
            </div>
          </div>
        </section>
        <section class="home__col">
          <h2 class="home__col__title">Planets</h2>
          <div class="home__col__list">
            <div v-for="planet in planets">
              <h3
                tabindex="0"
                @keyup.esc="closePopup"
                @click="(event) => handleClickPlanet(event)"
                :_id="planet._id"
                class="home__col__item"
              >
                {{ planet.name }}
              </h3>
            </div>
          </div>
        </section>
        <section class="home__col">
          <h2 class="home__col__title">Films</h2>
          <div class="home__col__list">
            <div v-for="film in films">
              <h3
                tabindex="0"
                @keyup.esc="closePopup"
                @click="(event) => handleClickFilm(event)"
                :_id="film._id"
                class="home__col__item"
              >
                {{ film.title }}
              </h3>
            </div>
          </div>
        </section>
      </main>
    </div>
  </div>
  <div class="stars"></div>
  <div class="twinkling"></div>
  <div class="clouds"></div>
  <nuxt-img src="/client-bg-2.png" class="home__background-img" />
</template>

<script setup>
  import { ref } from "vue";

  const state = ref({
    showCharacter: false,
    showFilm: false,
    showPlanet: false,
    character: {},
    film: {},
    planet: {},
  });

  const { data: charactersResponse } = await useFetch(
    "http://34.125.250.75:8000/characters"
  );
  const characters = ref(charactersResponse.value.data);

  const { data: planetsResponse } = await useFetch(
    "http://34.125.250.75:8000/planets"
  );
  const planets = ref(planetsResponse.value.data);

  const { data: filmsResponse } = await useFetch(
    "http://34.125.250.75:8000/films"
  );
  const films = ref(filmsResponse.value.data);

  function handleClickCharacter(event) {
    state.value.character = characters.value.find(
      (character) => character._id === event.target.attributes._id.value
    );
    state.value.showCharacter = !state.value.showCharacter;
  }

  function handleClickPlanet(event) {
    state.value.planet = planets.value.find(
      (planet) => planet._id === event.target.attributes._id.value
    );
    state.value.showPlanet = !state.value.showPlanet;
  }

  function handleClickFilm(event) {
    state.value.film = films.value.find(
      (film) => film._id === event.target.attributes._id.value
    );
    state.value.showFilm = !state.value.showFilm;
  }

  function closePopup() {
    state.value.showCharacter = false;
    state.value.showFilm = false;
    state.value.showPlanet = false;
  }
</script>

<style scoped>
  .home__card {
    height: 100vh;
    width: 100vw;
    background-color: rgba(0, 0, 0, 0.9);
    z-index: 100;
    position: relative;
    overflow-y: auto;
  }

  .home__background-img {
    width: 100%;
    z-index: 1;
    bottom: 0;
    position: absolute;
    opacity: 0;
    overflow: hidden;
    object-fit: cover;
  }
  .home {
    position: absolute;
    display: block;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    height: 100vh;
    z-index: 10;
    overflow: hidden;
  }

  .home__scroll {
    overflow-y: scroll;
    height: 100%;
    overflow-x: hidden;
  }

  .home__title {
    font-family: "Starjhol", sans-serif;
    color: rgb(255, 232, 31);
    font-size: clamp(2rem, 1.4886rem + 2.1818vw, 3.125rem);
    text-align: center;
  }

  .container {
    max-width: 900px;
    width: 100%;
    margin-inline: auto;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .home__body {
    display: flex;
    flex-direction: column;
    text-align: center;
    background: rgba(184, 237, 255, 0.05);
    border: solid 3px rgba(127, 222, 254, 0.05);
    border-radius: 15px;
  }

  .home__col {
    width: 60%;
  }

  .home__col__title {
    font-size: clamp(1.75rem, 1.5227rem + 0.9697vw, 2.25rem);
    font-weight: 700;
    margin: 0.3em 0em;
    color: #9effff;
    cursor: default;
  }

  .home__col__list {
    overflow-y: auto;
    max-height: 60vh;
  }

  .home__col__item {
    color: #9effff;
    background: rgba(184, 237, 255, 0.1);
    border: solid 1px #9effff;
    border-radius: 5px;
    padding: 6%;
    margin: 6%;
    cursor: pointer;
  }

  .home__col__item:hover {
    color: #c0f8f8;
    background: rgba(184, 237, 255, 0.568);
  }

  @media screen and (min-width: 900px) {
    .home__background-img {
      opacity: 100;
    }
    .home__scroll {
      overflow-y: auto;
    }
    .home__body {
      flex-direction: row;
      justify-content: space-between;
      align-items: start;
      animation: float 6s infinite alternate;
    }
  }
</style>
