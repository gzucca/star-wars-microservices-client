<template>
  <dialog id="characterDialog">
    <Card v-bind="characters" />
  </dialog>
  <div class="home">
    <div class="home__scroll">
      <header class="container">
        <h1 class="home__title">Star Wars Microservices</h1>
      </header>
      <main class="container main">
        <section class="main__col">
          <h2 class="main__col__title">Characters</h2>
          <div class="main__col__list">
            <div v-bind="characters" v-for="character in characters">
              <h3
                :birthYear="character.birth_year"
                v-bind="character"
                @click="(event) => handleClick(event)"
                class="main__col__list__item"
              >
                {{ character.name }}
              </h3>
            </div>
          </div>
        </section>
        <section class="main__col">
          <h2 class="main__col__title">Planets</h2>
          <div class="main__col__list">
            <div v-for="p in planets">
              <h3 class="main__col__list__item">{{ p.name }}</h3>
            </div>
          </div>
        </section>
        <section class="main__col">
          <h2 class="main__col__title">Films</h2>
          <div class="main__col__list">
            <div v-for="f in films">
              <h3 class="main__col__list__item">{{ f.title }}</h3>
            </div>
          </div>
        </section>
      </main>
    </div>
  </div>
  <div class="stars"></div>
  <div class="twinkling"></div>
  <div class="clouds"></div>
  <nuxt-img src="/client-bg-2.png" class="background" />
</template>

<script setup>
  import { ref, provide } from "vue";
  const { data: charactersResponse } = await useFetch(
    "http://34.125.250.75:8000/characters"
  );
  const characters = ref(charactersResponse.value.data);

  const { data: planetsResponse } = await useFetch(
    "http://34.125.250.75:8000/planets"
  );
  const planets = planetsResponse.value.data;

  const { data: filmsResponse } = await useFetch(
    "http://34.125.250.75:8000/films"
  );
  const films = filmsResponse.value.data;

  function handleClick(event) {
    console.log(event);
    characterDialog.showModal();
  }

  const setOpened = ref(false);
</script>

<style scoped>
  #characterDialog {
    height: 60vh;
    width: 70vw;
    padding: 0;
    border: solid 5px rgba(127, 222, 254, 0.875);
    background-color: rgba(255, 255, 255, 0);
    border-radius: 15px;
  }

  #characterDialog::backdrop {
    background-color: rgba(0, 0, 0, 0.733);
  }

  .background {
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
  .main {
    display: flex;
    flex-direction: column;
    text-align: center;
    background: rgba(184, 237, 255, 0.05);
    border: solid 3px rgba(127, 222, 254, 0.05);
    border-radius: 15px;
  }

  .main__col {
    width: 60%;
  }

  .main__col__title {
    font-size: clamp(1.75rem, 1.5227rem + 0.9697vw, 2.25rem);
    font-weight: 700;
    margin: 0.3em 0em;
    color: #9effff;
    cursor: default;
  }

  .main__col__list {
    overflow-y: auto;
    max-height: 60vh;
  }

  .main__col__list__item {
    color: #9effff;
    background: rgba(184, 237, 255, 0.1);
    border: solid 1px #9effff;
    border-radius: 5px;
    padding: 6%;
    margin: 6%;
    transform: rotateX(30deg);
    cursor: pointer;
  }

  .main__col__list__item:hover {
    color: #c0f8f8;
    background: rgba(184, 237, 255, 0.568);
  }

  @media screen and (min-width: 900px) {
    .background {
      opacity: 100;
    }
    .home__scroll {
      overflow-y: auto;
    }
    .main {
      flex-direction: row;
      justify-content: space-between;
      align-items: start;
      animation: float 6s infinite alternate;
    }
  }
</style>
