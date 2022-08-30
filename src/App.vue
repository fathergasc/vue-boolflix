<template>
  <div id="app">
    <MyHeader @search="getSearch"/>
    <MyMain :movies="movies"/>
  </div>
</template>

<script>
import MyHeader from './components/MyHeader.vue'
import MyMain from './components/MyMain.vue'

import axios from 'axios';

export default {
  name: 'App',
  
  components: {
    MyHeader,
    MyMain
  },
  data() {
    return {
      search: '',
      apiKey: 'cea5cb6798a2c2b6c1fac1af952cc7a4',
      moviesEndpoint:'https://api.themoviedb.org/3/search/movie?api_key=',
      movies: {},
    }
  },
  methods: {
    getSearch(search) {
      this.search = search;
      this.getMovies();
    },
    getMovies() {
            axios.get(this.moviesEndpoint + this.apiKey + '&query=' + this.search + '&language=it-IT')
                .then((response) => {
                    this.movies = response.data.results;
                })
        }
  }
}
</script>

<style lang="scss">

</style>
