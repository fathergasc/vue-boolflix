<template>
  <main>
    <div v-if="!movies.length == 0" class="wrap">
        <h1 class="section-title">MOVIES</h1>
        <div id="movies-container">
            <SingleCard v-for="(movie, index) in movies" :key="index" :cardData="movie" />
        </div>
    </div>
    
    
    <div v-if="!movies.length == 0" class="wrap">
        <h1 class="section-title">TV SERIES</h1>
        <div id="tvseries-container">
            <SingleCard v-for="(tvSeries, index) in tvSeries" :key="index" :cardData="tvSeries" />
        </div>
    </div>
    
    

  </main>
</template>

<script>

import SingleCard from './SingleCard.vue';

export default {


    name: 'MyMain',
    data() {
        return {
            posterURL: 'https://image.tmdb.org/t/p/w342'
        }
    },
    components: {
        SingleCard,
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

    body {
        background-color: #434343;
    }

    .w-20 {
        width: 20px;
    }

    #movies-container, #tvseries-container {
        
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        align-items: center;

        .flip-card {
            width: 342px;
            height: 513px;
            padding: 40px;

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
                    height: 40%;
                }
    }
        }
    }

    
    

    .section-title {
        text-align: center;
        margin-bottom: 20px;
    }

    
</style>