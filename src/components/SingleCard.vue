<template>
  <div class="flip-card">
    <div class="flip-card-inner">
      <div class="flip-card-front">
        <div class="no-poster" v-if="cardData.poster_path == null">
          <span>{{
            cardData.hasOwnProperty("title") ? cardData.title : cardData.name
          }}</span>
          <img
            class="no-poster-img"
            src="../assets/images/noposter.svg"
            alt=""
          />
        </div>
        <img
          class="poster-img"
          v-else
          :src="posterURL + cardData.poster_path"
          alt=""
        />
      </div>

      <div class="flip-card-back">
        <div class="title">
          <b>Titolo: </b
          >{{
            cardData.hasOwnProperty("title") ? cardData.title : cardData.name
          }}
        </div>
        <div v-if="cardData.title !== cardData.original_title || cardData.name !== cardData.original_name" class="original-title">
          <b>Titolo originale: </b
          >{{
            cardData.hasOwnProperty("original_title")
              ? cardData.original_title
              : cardData.original_name
          }}
        </div>
        <div class="lang-card">
          <img
            class="w-30"
            :src="flagEndpoint + convertLangToFlag(cardData.original_language)"
          />
        </div>
        <span v-html="convertRating(cardData.vote_average)"></span>
        <p>{{ cardData.overview }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "SingleCard",
  props: {
    cardData: Object,
  },
  data() {
    return {
      posterURL: "https://image.tmdb.org/t/p/w342",
      flagEndpoint: "https://countryflagsapi.com/png/",
    };
  },
  methods: {
    convertLangToFlag(lang) {
      if (lang == "en") {
        return "gb";
      } else if (lang == "ja") {
        return "jp";
      } else if (lang == "ko") {
        return "kr";
      } else if (lang == "zh") {
        return "cn";
      } else if (lang == "sv") {
        return "se";
      } else if (lang == "da") {
        return "dk";
      } else if (lang == "el") {
        return "gr";
      } else if (lang == "cs") {
        return "cz";
      } else if (lang == "sl") {
        return "si";
      } else {
        return lang;
      }
    },
    convertRating(rating) {
      let starsRating = [];
      if (rating == 0) {
        starsRating.push("Senza voto");
        return starsRating.join("");
      } else {
        rating = Math.round(rating) / 2;

        for (let i = rating; i >= 1; i--) {
          if (i == 1.5) {
            starsRating.push('<i class="fa-solid fa-star"></i>');
            starsRating.push('<i class="fa-regular fa-star-half-stroke"></i>');
          } else {
            starsRating.push('<i class="fa-solid fa-star"></i>');
          }
        }
        for (let i = 5 - rating; i >= 1; i--) {
          starsRating.push('<i class="fa-regular fa-star"></i>');
        }
        starsRating = starsRating.join("");
        return starsRating;
      }
    },
  },
};
</script>

<style lang="scss">
@import "~@fortawesome/fontawesome-free/css/all.css";
@import "@/styles/vars.scss";

.no-poster {
  position: relative;
  span {
    position: absolute;
    top: 10px;
    text-align: center;
    font-size: 22px;
    font-weight: bold;
    padding: 0 5px;
  }
}

.flip-card {
    margin-top: 40px;
  background-color: transparent;
  perspective: 1000px;
  width: $card-width;
  height: $card-height;
  margin: 20px;
  .poster-img {
    width: 100%;
    height: 100%;
  }

  span {
    font-weight: bold;
  }

  .no-poster-img {
    width: $card-width;
    height: $card-height;
  }

  .lang-card {
    margin: 10px 0;
    height: 30px;
    display: block;
    text-transform: uppercase;
    display: flex;
    align-items: center;
  }

  .no-poster {
    width: $card-width;
    height: $card-height;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #ccc;

    img {
      height: 40%;
    }
  }
}

.flip-card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: left;
  transition: transform 0.8s;
  transform-style: preserve-3d;
}

.flip-card:hover .flip-card-inner {
  transform: rotateY(180deg);
}

.flip-card-front,
.flip-card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
  box-shadow: 10px 12px 10px -2px rgb(26, 25, 25);
}

.flip-card-front {
  background-color: transparent;
  color: black;
}

.flip-card-back {
  padding: 15px;
  background-color: black;
  color: white;
  transform: rotateY(180deg);
  overflow: auto;

  p {
    padding-top: 10px;
    font-size: 1rem;
    text-align: left;
  }

  i {
    color: gold;
    font-size: 20px;
  }
}

.title {
  font-size: 20px;
}

.original-title {
  margin: 15px 0;
}
</style>