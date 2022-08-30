<template>
  <div>
    <ul v-for="(movie, index) in movies" :key="index">
        <li>
            <h4>{{movie.title}}</h4>
            <h5>{{movie.original_title}}</h5>
            <h5>{{movie.original_language}}</h5>
            <h5>{{movie.vote_average}}</h5>
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
}
</script>

<style>

</style>