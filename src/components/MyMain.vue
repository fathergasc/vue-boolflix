<template>
  <main>
    <h1>MOVIES</h1>
    <div id="movies-container">
        
        <ul class="list" v-for="(movie, index) in movies" :key="index">
            <li>
                <div class="no-poster" v-if="movie.poster_path == null">
                    <img src="../assets/images/noposter.svg" alt="">
                </div>
                <img v-else :src="posterURL + movie.poster_path" alt="">
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
    <h1>TV SERIES</h1>
    <div id="tvseries-container">
        
        <ul class="list" v-for="(tvseries, index) in tvSeries" :key="index">
            <li>
                <div class="no-poster" v-if="tvseries.poster_path == null">
                    <img src="../assets/images/noposter.svg" alt="">
                </div>
                <img v-else :src="posterURL + tvseries.poster_path" alt="">
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
            posterURL: 'https://image.tmdb.org/t/p/w342'
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

    ul {
        min-width: 342px;
        list-style: none;
    }

    #movies-container, #tvseries-container {
        
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        align-items: center;

        li {
            width: 100%;
        }
    }

    .no-poster {
        width: 100%;
        height: 513px;
        display: flex;
        justify-content: center;
        align-items: center;
        background-color: #ccc;

        img {
            width: 60%;
        }
    }

    
</style>