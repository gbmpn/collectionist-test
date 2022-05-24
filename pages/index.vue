<template>
  <div class="grid-movies">

    <section class="banner-movie">
      <h2>{{backgroundMovie.original_title}}</h2>
      <img :src="`https://image.tmdb.org/t/p/original/` + backgroundMovie.backdrop_path" alt="">
    </section>

    <section class="trending">
      <span class="bgTitle">trending</span>
      <ul class="container mx-auto mt-20 grid grid-cols-4 gap-4">
          <li class="p-6" v-for="(film, i) in listFilms" :key="i" v-if="listFilms && listFilms.length > 0 && i <= limit">
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
import axios from 'axios'

export default {
  name: 'Index',
  data() {
    return {
      listFilms: [],
      limit: 3,
      backgroundMovie: []
    }
  },
  created() {
    axios
      .get(`https://api.themoviedb.org/3/movie/550?api_key=d59e0d2216b36ac1309410441fbcedb6`)
      .then(response => {
          this.backgroundMovie = response.data
          console.log(this.backgroundMovie)
      })

    axios
      .get(`https://api.themoviedb.org/3/trending/all/week?api_key=d59e0d2216b36ac1309410441fbcedb6`)
      .then(response => {
          this.listFilms = response.data.results
      })
  }
}
</script>

<style>
.grid-movies {
  padding-top: 80px;
}
.banner-movie{
  width: 100%;
  height: 80vh;
  display: block;
  position: relative;
  overflow: hidden;
}
.banner-movie img {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
}
.banner-movie h2{
  position: absolute;
  bottom: 0;
  left: 0;
  z-index: 2;
  font-size: 5em;
  padding: 1.5rem;
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
