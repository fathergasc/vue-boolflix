<template>
  <main>
    <div v-if="!movies.length == 0" class="wrap">
        <h1 class="section-title">MOVIES</h1>
        <div  id="movies-container">
        <div class="list" v-for="(movie, index) in movies" :key="index">
            <div class="card">
                <div class="no-poster" v-if="movie.poster_path == null">
                    <img class="no-poster-img" src="../assets/images/noposter.svg" alt="">
                </div>
                <img  class="poster-img" v-else :src="posterURL + movie.poster_path" alt="">
                <h4>{{movie.title}}</h4>
                <h5>{{movie.original_title}}</h5>
                <div class="lang-card" v-if="movie.original_language == 'en'">
                    <img  class="w-20" src="../assets/images/gb.svg" alt="">
                </div>
                <div class="lang-card" v-else-if="movie.original_language == 'it'">
                    <img class="w-20" src="../assets/images/it.svg" alt="">
                </div>
                <h5 class="lang-card" v-else>{{movie.original_language}}</h5>
                <h5 v-html="convertRating(movie.vote_average)"></h5>
                <img src="" alt="">
            </div>
        </div>
    </div>
    </div>
    
    
    <div v-if="!movies.length == 0" class="wrap">
        <h1 class="section-title">TV SERIES</h1>
        <div  id="tvseries-container">
        
        <div class="list" v-for="(tvseries, index) in tvSeries" :key="index">
            <div class="card">
                <div class="no-poster" v-if="tvseries.poster_path == null">
                    <img class="no-poster-img" src="../assets/images/noposter.svg" alt="">
                </div>
                <img class="poster-img" v-else :src="posterURL + tvseries.poster_path" alt="">
                <h4>{{tvseries.title}}</h4>
                <h5>{{tvseries.original_name}}</h5>
                <div class="lang-card" v-if="tvseries.original_language == 'en'">
                    <img class="w-20" src="../assets/images/gb.svg" alt="">
                </div>
                <div class="lang-card" v-else-if="tvseries.original_language == 'it'">
                    <img class="w-20" src="../assets/images/it.svg" alt="">
                </div>
                <h5 class="lang-card" v-else>{{tvseries.original_language}}</h5>
                <h5 v-html="convertRating(tvseries.vote_average)"></h5>
                <img src="" alt="">
            </div>
        </div>
    </div>
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
            rating = Math.round(rating) / 2;
            let starsRating = [];

            for (var i = rating; i >= 1; i--) 
                starsRating.push('<i class="fa-solid fa-star"></i>');
                if (i == .5) starsRating.push('<i class="fa-regular fa-star-half-stroke"></i>');
            
            for (let i = (5 - rating); i >= 1; i--)
            starsRating.push('<i class="fa-regular fa-star"></i>');
            

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

    .list {
        min-width: 342px;
    }

    #movies-container, #tvseries-container {
        
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        align-items: center;

        .card {
            width: 342px;
            height: 800px;
            padding: 10px;

            .poster-img {
                height: 513px;
                width: 342px;
            }

            .no-poster-img {
                height: 513px;
            }
            
            .lang-card {
                height: 30px;
            }

            .no-poster {
                width: 342px;
                height: 513px;
                display: flex;
                justify-content: center;
                align-items: center;
                background-color: #ccc;

                img {
                    height: 60%;
                }
    }
        }
    }

    
    

    .section-title {
        text-align: center;
        margin-bottom: 20px;
    }

    
</style>