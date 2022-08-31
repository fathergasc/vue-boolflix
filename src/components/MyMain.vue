<template>
  <main>
    
    <div v-if="!movies.length == 0" id="movies-container">
        <h1 >MOVIES</h1>
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
                <h5>{{convertRating(movie.vote_average)}}</h5>
                <img src="" alt="">
            </li>
        </ul>
    </div>
    
    <div v-if="!movies.length == 0" id="tvseries-container">
        <h1>TV SERIES</h1>
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
                <h5>{{convertRating(tvseries.vote_average)}}</h5>
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
        convertRating(rating) {
            rating = Math.round(rating * 2) / 2;
            let starsRating = [];

            for (var i = rating; i >= 1; i--) {
                starsRating.push('<i class="fa-solid fa-star"></i>');
                if (i == .5) starsRating.push('<i class="fa-regular fa-star-half-stroke"></i>');
            }
            for (let i = (5 - rating); i >= 1; i--){
            starsRating.push('<i class="fa-regular fa-star"></i>');
            }

            starsRating = starsRating.join('');
            return starsRating;
        }
    }
}
</script>

<style lang="scss">

@import '~@fortawesome/fontawesome-free/css/all.css';

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