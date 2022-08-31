<template>
        <div class="card">
            <div class="no-poster" v-if="cardData.poster_path == null">
                <img class="no-poster-img" src="../assets/images/noposter.svg" alt="">
            </div>
            <img  class="poster-img" v-else :src="posterURL + cardData.poster_path" alt="">
            <h4>{{(cardData.hasOwnProperty('title'))? cardData.title : cardData.name}}</h4>
            <h5>{{(cardData.hasOwnProperty('original_title'))? cardData.original_title : cardData.original_name}}</h5>
            <div class="lang-card" v-if="cardData.original_language == 'en'">
                <img  class="w-20" src="../assets/images/gb.svg" alt="">
            </div>
            <div class="lang-card" v-else-if="cardData.original_language == 'it'">
                <img class="w-20" src="../assets/images/it.svg" alt="">
            </div>
            <h5 class="lang-card" v-else>{{cardData.original_language}}</h5>
            <h5 v-html="convertRating(cardData.vote_average)"></h5>
            <img src="" alt="">
        </div>
  
</template>

<script>
export default {
    name: 'SingleCard',
    props: {
        cardData: Object,
    },
    data() {
        return {
            posterURL: 'https://image.tmdb.org/t/p/w342'
        }
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
    },
}
</script>

<style lang="scss">


@import '~@fortawesome/fontawesome-free/css/all.css';

    
</style>