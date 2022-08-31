<template>
  <div id="app">
    <MyHeader @search="getSearch"/>
    <MyMain :movies="movies" :tvSeries="tvSeries"/>
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
      movies: [],
      tvSeries: [],
      tvSeriesEndpoint: 'https://api.themoviedb.org/3/search/tv?api_key='
    }
  },
  methods: {
    getSearch(search) {
      this.search = search;
      this.getMovies();
      this.getTvSeries();
    },
    getMovies() {
            axios.get(this.moviesEndpoint + this.apiKey + '&query=' + this.search + '&language=it-IT')
                .then((response) => {
                    this.movies = response.data.results;
                })
        },
    getTvSeries() {
            axios.get(this.tvSeriesEndpoint + this.apiKey + '&query=' + this.search + '&language=it-IT')
                .then((response) => {
                    this.tvSeries = response.data.results;
                })
        },
  }
}
</script>

<style lang="scss">

@import './styles/common.scss'

</style>
