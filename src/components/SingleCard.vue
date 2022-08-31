<template>
    <div class="flip-card">
        <div class="flip-card-inner">
            <div class="flip-card-front">
                <div class="no-poster" v-if="cardData.poster_path == null">
                    <span>{{(cardData.hasOwnProperty('title'))? cardData.title : cardData.name}}</span>
                    <img class="no-poster-img" src="../assets/images/noposter.svg" alt="">
                 </div>
                <img  class="poster-img" v-else :src="posterURL + cardData.poster_path" alt="">
            </div>

            <div class="flip-card-back">
                <h1>Titolo: {{(cardData.hasOwnProperty('title'))? cardData.title : cardData.name}}</h1>
                <h3>Titolo originale: {{(cardData.hasOwnProperty('original_title'))? cardData.original_title : cardData.original_name}}</h3>
                <div class="lang-card" v-if="cardData.original_language == 'en'">
                    <img  class="w-20" src="../assets/images/gb.svg" alt="">
                </div>
                <div class="lang-card" v-else-if="cardData.original_language == 'it'">
                    <img class="w-20" src="../assets/images/it.svg" alt="">
                </div>
                <div class="lang-card" v-else>{{cardData.original_language}}</div>
                <span v-html="convertRating(cardData.vote_average)"></span>
                <p>{{cardData.overview}}</p>
            </div>
            
            
        </div>
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

.no-poster {
    position: relative;
    span {
        position: absolute;
        top: 80px;
        left: 50%;
        font-size: 30px;
        font-weight: bold;
        transform: translate(-50%, -50%);
    }

}

.flip-card {
    background-color: transparent;
    perspective: 1000px;
}
.flip-card-inner {
    position: relative;
    width: 100%;
    height: 100%;
    text-align: center;
    transition: transform 0.8s;
    transform-style: preserve-3d;
}

.flip-card:hover .flip-card-inner {
    transform: rotateY(180deg);
}

.flip-card-front, .flip-card-back {
    position: absolute;
    width: 100%;
    height: 100%;
    -webkit-backface-visibility: hidden;
    backface-visibility: hidden;
}

.flip-card-front {
    background-color: transparent;
    color: black;
}

.flip-card-back {
    padding: 10px;
    background-color: black;
    color: white;
    transform: rotateY(180deg);
    overflow: auto;

    p {
        font-size: 18px;
    }
}
    
</style>