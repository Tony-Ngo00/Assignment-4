<template>
  <h1>NOTflix</h1>

  <div class="movie-container">
    <label id = "selection" for="Movies">Choose a Movie:</label>
    <select v-model="movie">
      <option value="810693">Jujutsu Kaisen 0</option>
      <option value="635302">Demon Slayer - Kimetsu no Yaiba- The Movie: Mugen Train</option>
      <option value="768744">My Hero Academia: World Heroes' Mission</option>
      <option value="843241">The Seven Deadly Sins: Cursed by Light</option>
      <option value="900667">One Piece Film Red</option>
      <option value="553610">Mobile Suit Gundam Narrative</option> 
      <option value="347201">Boruto: Naruto the Movie</option>  
      <option value="303857">Dragon Ball Z: Resurrection 'F'</option>
      <option value="503314">Dragon Ball Super: Broly</option>
      <option value="610150">Dragon Ball Super: Super Hero</option> 
    </select>
    <button id="getButton" @click=selectOption()>Get</button>
  </div>
  <body>
  <div v-show="hide">
    <table>
      <tr>
        <td id="left">
          <img :src="poster">
        </td>
        <td id="right" >
          <p id="info">Title: {{title}}</p>
          <p id="info">Original Title: {{originalTitle}}</p>
          <p id="special" class="indent">Genre:</p>
          <p id="special" v-for="genre in genres" style="display: inline">-{{genre.name}}- </p>
          <p id="info">Release Date: {{releaseDate}}</p>
          <p id="info">Popularity: {{popularity}}</p>
          <p id="info">Revenue: {{revenue}}</p>
          <p id="info">Vote Average: {{voteAverage}}</p>
          <p id="info">Cote Count: {{voteCount}}</p>
          <p id="info">Runtime: {{runtime}} mins</p>
          <p id="overviewLabel">Overview:</p>
          <p id="overviewText">{{overviewText}}</p> 
          <iframe :src="video"></iframe>
        </td>
      </tr>
    </table>
  </div>
</body>
</template>

<script setup>
  import axios from "axios";
  import { ref } from 'vue';

  let hide = ref(false);
  
  const movie = ref(810693);

  let poster = ref("");
  let title = ref("");
  let originalTitle = ref("");
  let genres = ref([]);
  let releaseDate = ref("");
  let popularity = ref("");
  let revenue = ref("");
  let voteAverage = ref("");
  let voteCount = ref("");
  let runtime = ref("");
  let overviewText = ref("");
  let video = ref("");

  function selectOption() {
    let searchMovie = axios.get(`https://api.themoviedb.org/3/movie/${movie.value}`, {
      params: {
          api_key: "779ebe30f392f779f18a739e5df2f414",
          append_to_response: "videos",
      }
    })
    console.log(searchMovie);

    function formatPrice(value) {
        var formatter = new Intl.NumberFormat('en-US', {
          style: 'currency',
          currency: 'USD',
        });
        return formatter.format(value);
    }
    let movieInfo = searchMovie.then((movieData) => {
      poster.value = "https://image.tmdb.org/t/p/w500" + movieData.data.poster_path;
      title.value = movieData.data.title;
      originalTitle.value = movieData.data.original_title;
      genres.value = movieData.data.genres;
      popularity.value = movieData.data.popularity;
      revenue.value = formatPrice(movieData.data.revenue);
      voteAverage.value = movieData.data.vote_average;
      voteCount.value = movieData.data.vote_count;
      runtime.value = movieData.data.runtime;
      overviewText.value = movieData.data.overview;
      video.value = "https://www.youtube.com/embed/" + (movieData.data.videos.results.filter((trailer) => trailer.type === "Trailer")).at(0).key;
      hide = ref(true);
    })
    
  }
</script>

<style scoped>
  h1 {
    padding-left: 20px;
    color: rgb(202, 26, 26);
    font-weight: bold;
    font-size: 50px;
    font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
  }

  movies {
    padding-left: 20px;
    color: rgb(202, 26, 26);
    font-weight: bold;
    font-family: 'Courier New', Courier, monospace;
    font-size: 20px;
  }

  #selection {
    padding-left: 20px;
    color: rgb(202, 26, 26);
    font-weight: bold;
    font-family: 'Courier New', Courier, monospace;
    font-size: 20px;
  }

  select {
    margin-left: 4px;
    text-align: center;
    color: rgb(202, 26, 26);
    background-color: rgb(54, 52, 52);
    border-color: rgba(71, 70, 70, 0.76);
    font-weight: bold;
    font-family: 'Courier New', Courier, monospace;
    font-size: 20px;
  }

  button {
    margin-left: 4px;
    font-size: 20px;
    color: rgb(202, 26, 26);
    background-color: rgb(54, 52, 52);
    border-color: rgba(71, 70, 70, 0.76);
    border-width: 3px;
  }

  table {
    width: 1229px;
    height: 850px;
    margin-top: 1rem;
    margin-left: 1rem;
    padding-left: 0%;
    padding-right: 0%;
    padding-top: 1rem;
    padding-bottom: 1rem;
    background-color: rgb(0, 0, 0);
  }

  #info {
    margin-top: 0%;
    padding-left: 20px;
    padding-bottom: 0%;
    margin-bottom: 0%;
    color: rgb(196, 67, 67);
    font-weight: bold;
    font-family: 'Courier New', Courier, monospace;
  }

  #special {
    margin: 0%;
    display:inline;
    margin-top: 0%;
    padding-left: 20px;
    padding-bottom: 0%;
    margin-bottom: 0%;
    color: rgb(196, 67, 67);
    font-weight: bold;
    font-family: 'Courier New', Courier, monospace;
  }

  #overviewLabel {
    padding-left: 20px;
    padding-top: 10px;
    padding-bottom: 0%;
    margin-top: 0%;
    margin-bottom: 0%;
    color: rgb(196, 67, 67);
    font-weight: bold;
    font-family: 'Courier New', Courier, monospace;
  }

  #overviewText {
    padding-left: 20px;
    margin-top: 0%;
    color: rgb(196, 67, 67);
    width: 660px;
    font-weight: bold;
    font-family: 'Courier New', Courier, monospace;
  }

  img {
    margin-left: 20px;
    margin-top: 0%;
    width: 500px;
    height: 700px;
  }

  iframe {
    margin-left: 20px;
    height: 370px;
    aspect-ratio: 16/9;
    border-width: 5px;
    border-color: rgba(71, 70, 70, 0.76);
  }
</style>
