<template>
    <div class="movie-detail">
        <h2>{{movie.Title}}</h2>
        <p>{{ movie.Year }}</p>
        <img :src="movie.Poster" alt="Movie Poster" class="featured-img" />
        <h3>Rating : {{ movie.imdbRating }}/10</h3>
        <h3>BoxOffice : {{ movie.BoxOffice }}</h3>
        <p>{{ movie.Plot }}</p>
    </div>
</template>

<script >
import { ref, onBeforeMount } from 'vue';
import { useRoute } from 'vue-router';
import env from '@/env.js';

export default {
    setup() {
        const movie = ref({});
        const route = useRoute();


        onBeforeMount(() =>{
            console.log("before Mount")
            fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`)
            .then(response => response.json())
            .then(data =>{
                // console.log(data);
                movie.value = data;
            });

        });
        return {
            movie
        }
    }
}

</script>

<style lang="scss">
.movie-detail {
  padding: 16px;

  h2 {
    color: #FFF;
    font-size: 28px;
    font-weight: 600;
    margin-bottom: 16px;
  }
  
  .featured-img {
    display: block;
    max-width: 200px;
    margin-bottom: 16px;
  }
  p {
    color: #FFF;
    font-size: 18px;
    line-height: 1.4;
  }
}
</style>
