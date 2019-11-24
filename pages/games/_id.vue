<template>
    <div class="container mx-auto">
        <img :src="game.cover.url.replace('t_thumb', 't_cover_big')" alt="cover">
        <div>
            <h2>{{ game.name }}</h2>
        </div>
        <div v-for="genre in game.genres" :key="genre.id">
            <p>{{ genre.name }}</p>
        </div>
    </div>
</template>

<script>
import axios from "axios";

export default {

    asyncData ({ params, error }) {

    const proxtUrl = 'https://cors-anywhere.herokuapp.com/'

    return axios.get(`${proxtUrl}https://api-v3.igdb.com/games/${params.id}/?fields=name,cover.url,genres.name,summary,platforms.name,first_release_date,websites.url,total_rating,screenshots.url&expand=genres,cover,platforms,websites,screenshots`)
      .then((res) => {
        return { 
          game: res.data[0]
        }
      })
      .catch((e) => {
        console.log(e)
      })
  },
  data() {
    return {

    }
  }
}
</script>