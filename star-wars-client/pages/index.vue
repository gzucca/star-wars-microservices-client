<template>
  <div class="home">
    <div class="home__scroll">
      <header class="container">
        <h1 class="home__title">Star Wars Microservices</h1>
      </header>
      <main class="container main">
        <section class="main__col">
          <h2 class="main__col__title">Characters</h2>
          <div class="main__col__list">
            <div v-for="c in characters">
              <h3>{{ c.name }}</h3>
            </div>
          </div>
        </section>
        <section class="main__col">
          <h2 class="main__col__title">Planets</h2>
          <div class="main__col__list">
            <div v-for="p in planets">
              <h3>{{ p.name }}</h3>
            </div>
          </div>
        </section>
        <section class="main__col">
          <h2 class="main__col__title">Films</h2>
          <div class="main__col__list">
            <div v-for="f in films">
              <h3>{{ f.title }}</h3>
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
  const { data: charactersResponse } = await useFetch(
    "http://34.125.250.75:8000/characters"
  );
  const characters = charactersResponse.value.data;

  const { data: planetsResponse } = await useFetch(
    "http://34.125.250.75:8000/planets"
  );
  const planets = planetsResponse.value.data;

  const { data: filmsResponse } = await useFetch(
    "http://34.125.250.75:8000/films"
  );
  const films = filmsResponse.value.data;
</script>

<style scoped>
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
    background-color: purple;
  }

  .main__col {
    width: 60%;
    background-color: blue;
  }

  .main__col__title {
    font-size: clamp(1.75rem, 1.5227rem + 0.9697vw, 2.25rem);
    font-weight: 700;
    margin: .3em 0em;
  }

  .main__col__list {
    overflow-y: auto;
    max-height: 60vh;
    background-color: red;
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
    }
  }
</style>
