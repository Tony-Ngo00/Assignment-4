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
  <div id="display">
    <table>
      <tr>
        <td id="left">
          <img id="cover">
        </td>
        <td id="right">
          <p id="info"></p>
          <p id="basicInfo"></p>
          <p id="vote"></p>
          <p id="overviewLabel"></p>
          <p id="overviewText"></p> 
          <iframe id="video"></iframe>
        </td>
      </tr>
    </table>
  </div>
</body>
</template>

<script setup>
  import axios from "axios";
  import { ref } from 'vue';
  
  const movie = ref(810693);
  const display = ref("");
  const info = ref("");
  const overviewLabel = ref("");
  const overviewText = ref("");
  const cover = ref("");
  const video = ref("");

  function selectOption() {
    let searchMovie = axios.get(`https://api.themoviedb.org/3/movie/${movie.value}`, {
      params: {
          api_key: "779ebe30f392f779f18a739e5df2f414",
          append_to_response: "videos",
      }
    })
    console.log(movie.value);

    let infoResults = searchMovie.then((selectedMovie) => {       
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           
    })
  }
</script>

<style scoped>
  body {
  background-color: rgba(0, 0, 0, 0.856);
  }

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

</style>
