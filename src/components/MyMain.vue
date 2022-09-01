<template>
  <main>
    <div v-if="!movies.length == 0" class="wrap">
      <h1 class="section-title">Film</h1>
      <div class="separator"></div>
      <div id="movies-container">
        <SingleCard
          v-for="(movie, index) in movies"
          :key="index"
          :cardData="movie"
        />
      </div>
    </div>

    <div v-if="!tvSeries.length == 0" class="wrap">
      <h1 class="section-title">Serie TV</h1>
      <div class="separator"></div>
      <div id="tvseries-container">
        <SingleCard
          v-for="(tvSeries, index) in tvSeries"
          :key="index"
          :cardData="tvSeries"
        />
      </div>
    </div>
  </main>
</template>

<script>
import SingleCard from "./SingleCard.vue";

export default {
  name: "MyMain",
  data() {
    return {
      posterURL: "https://image.tmdb.org/t/p/w342",
    };
  },
  components: {
    SingleCard,
  },
  props: {
    movies: Array,
    tvSeries: Array,
  },
  methods: {
    convertRating(rating) {
      rating = Math.round(rating) / 2;
      let starsRating = [];

      for (var i = rating; i >= 1; i--)
        starsRating.push('<i class="fa-solid fa-star"></i>');
      if (i == 0.5)
        starsRating.push('<i class="fa-regular fa-star-half-stroke"></i>');

      for (let i = 5 - rating; i >= 1; i--)
        starsRating.push('<i class="fa-regular fa-star"></i>');

      starsRating = starsRating.join("");
      return starsRating;
    },
  },
};
</script>

<style lang="scss">
@import "~@fortawesome/fontawesome-free/css/all.css";

#movies-container,
#tvseries-container {
  max-width: 1450px;
  margin: 0 auto;
  display: flex;
  flex-wrap: wrap;
  justify-content: flex-start;
  align-items: center;
}

.section-title {
  text-align: center;
  margin-bottom: 20px;
  color: white;
}

.separator {
  width: 100%;
  height: 3px;
  background-color: white;
  margin: 20px 0;
}
</style>