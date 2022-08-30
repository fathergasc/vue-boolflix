<template>
  <main>
    <div id="movies-container">
        <h1>MOVIES</h1>
        <ul v-for="(movie, index) in movies" :key="index">
            <li>
                <h4>{{movie.title}}</h4>
                <h5>{{movie.original_title}}</h5>
                <div v-if="movie.original_language == 'en'">
                    <img class="w-20" src="../assets/images/gb.svg" alt="">
                </div>
                <div v-else-if="movie.original_language == 'it'">
                    <img class="w-20" src="../assets/images/it.svg" alt="">
                </div>
                <h5 v-else>{{movie.original_language}}</h5>
                <h5>{{movie.vote_average}}</h5>
                <img src="" alt="">
            </li>
        </ul>
    </div>
    <div class="tvseries-container">
        <h1>TV SERIES</h1>
        <ul v-for="(tvseries, index) in tvSeries" :key="index">
            <li>
                <h4>{{tvseries.title}}</h4>
                <h5>{{tvseries.original_name}}</h5>
                <div v-if="tvseries.original_language == 'en'">
                    <img class="w-20" src="../assets/images/gb.svg" alt="">
                </div>
                <div v-else-if="tvseries.original_language == 'it'">
                    <img class="w-20" src="../assets/images/it.svg" alt="">
                </div>
                <h5 v-else>{{tvseries.original_language}}</h5>
                <h5>{{tvseries.vote_average}}</h5>
                <img src="" alt="">
            </li>
        </ul>
    </div>
    

  </main>
</template>

<script>



export default {


    name: 'MyMain',
    data() {
        return {
            
        }
    },
    props: {
        movies: Array,
        tvSeries: Array
    },
    methods: {
    }
}
</script>

<style lang="scss">
    .w-20 {
        width: 20px;
    }
</style>