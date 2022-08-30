<template>
  <div>
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
</template>

<script>



export default {


    name: 'MyMain',
    data() {
        return {
            
        }
    },
    props: {
        movies: Object
    },
    methods: {
        getImg(path){
            return require('../assets/images/' + path);
        },
        langToFlag(lang) {
            switch (lang) {
                case 'en':
                return 'gb.svg';
                case 'it':
                return 'it.svg';
                default:
                return lang;
                
            }
        }
    }
}
</script>

<style lang="scss">
    .w-20 {
        width: 20px;
    }
</style>