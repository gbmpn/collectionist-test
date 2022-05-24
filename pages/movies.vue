<template>
  <div class="grid-movies">
    <nav>
      <button class="m-6" @click="updateGenre(28)">Action</button>
      <button class="m-6" @click="updateGenre(16)">Animation</button>
      <button class="m-6" @click="updateGenre(12)">Aventure</button>
      <button class="m-6" @click="updateGenre(35)">Comédie</button>
      <button class="m-6" @click="updateGenre(99)">Documentaire</button>
    </nav>
    
    <section class="trending">
      <span class="bgTitle">movies</span>
      <ul class="container mx-auto mt-20 grid grid-cols-4 gap-4">
          <li class="p-6" v-for="(film, i) in listFilms" :key="i">
              <BaseCard
              :url="film.poster_path"
              :title="film.original_title"
              :vote="film.vote_average"
            ></BaseCard>
          </li>
      </ul>
    </section>
  </div>
</template>

<script>
import { log } from 'console'
import axios from 'axios'

export default {
  name: 'Movie',
  data() {
    return {
      listFilms: [],
      currentGenre: 28
    }
  },
  created() {
    axios
      .get(`https://api.themoviedb.org/3/discover/movie?api_key=d59e0d2216b36ac1309410441fbcedb6&language=en-US&with_genres=${this.currentGenre}`)
      .then(response => {
          this.listFilms = response.data.results
      })
  },
  methods: {
    updateGenre(genreid) {
      console.log(genreid);
      axios
      .get(`https://api.themoviedb.org/3/discover/movie?api_key=d59e0d2216b36ac1309410441fbcedb6&language=en-US&with_genres=${genreid}`)
      .then(response => {
          this.listFilms = response.data.results
      })
    }
  }
}
</script>

<style>
.grid-movies {
  padding-top: 80px;
}

nav button {
  border: solid 1px #fff;
  padding: 10px;
  border-radius: 20px;
}

.trending {
  position: relative;
}

.trending span.bgTitle{
  font-size: 20vw;
  position: absolute;
  left: 1.5rem;
  top: -25vh;
  color: transparent;
  -webkit-text-stroke: 0.5px #fff;
  font-weight: bold;
  z-index: -1;
}
</style>
