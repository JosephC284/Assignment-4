<script setup>
import axios from "axios";
import { ref } from "vue";

const movieId = ref(null);
const movieData = ref(null);

const retriveInfo = async () => {
  movieData.value = await axios.get(`https://api.themoviedb.org/3/movie/${movieId.value}`, {
    params: {
      api_key: "09a6e007d7a19baca792f4031cd63246",
      append_to_response: "videos",
    }  
  })
};


</script>

<template>
<body>
  <div class="selector">
    <label for="movies">Information on Movies:</label>
      <div>
        <select v-model = "movieId">
          <option value="299534">Avengers Endgame</option>
          <option value="299536">Avengers Infinity War</option>
          <option value="99861">Avengers Age of Ultron</option>
          <option value="24428">The Avengers</option>
          <option value="102899">Ant-Man</option>
          <option value="271110 ">Captain America: Civil War</option>
          <option value="566525">Shang Chi and the Legend of the Ten Rings</option>
          <option value="283995">Guardians of the Galaxy Vol. 2</option>
          <option value="10138">Iron Man 2</option>
          <option value="284053">Thor Ragnarok</option>
        </select>
      </div>
    <input type="button" value=" Get " @click="retriveInfo">
  </div>
  <div v-if="movieData" id="output">
    <iframe :src="`https://www.youtube.com/embed/${movieData.data.videos.results.filter((trailer) => trailer.type === 'Trailer').at(0).key}`" />   
    <img :src="`https://image.tmdb.org/t/p/w500${movieData.data.poster_path}`" /> 
    <p>Movie Title:  {{movieData.data.title}}</p>
    <p>Release Date: {{movieData.data.release_date}}</p>
    <p>Popularity: {{movieData.data.popularity}}</p>
    <p>Movie Id: {{movieData.data.id}}</p>
    <p>Movie Overview: {{movieData.data.overview}}</p>
    <p>Movie Vote Count: {{movieData.data.vote_count}}</p>
    <p>Movie Status: {{movieData.data.status}}</p>
    <p>Movie Revenue: {{movieData.data.revenue}}</p>
    <p>Movie Budget: {{movieData.data.budget}}</p>  
  </div>
</body>
</template>

<style> 
* {
  padding: 0px;
  margin: 0px;
  box-sizing: border-box;
}

.selector {
  background-color: skyblue;
  border: 5px;
  border-style: solid;
  border-color: black;
  font-size: 40px;
  margin-left: 20%;
  margin-right: 20%;
  padding: 0px;
  text-align: center;
}

#output {
  display: block;
  margin-left: 20%;
  margin-right: 20%;
  border-style: solid;
  border-width: 5px;
  background-color: skyblue;

  ;
}

p {
  border-style: solid;
  border-width: 5px;
  background-color: mediumblue;
  display: block;
  margin: 10px;
  text-align: center;
  font-family: Arial, Helvetica, sans-serif;
  color: white;
  padding: 5px;
}

img {
  display: block;
  margin-top: 5px;
  margin-left: auto;
  margin-right: auto;
  width: 200px;
  height: 300px;
}

iframe {
  display: block;
  margin-top: 5px;
  margin-left: auto;
  margin-right: auto;
  height: 300px;
  width: 500px;
}

body {
  background-color: midnightblue;
}

label {
  font-family: Impact, 'Haettenschweiler', sans-serif;
  color: white;
}

select {
  font-family: Impact, 'Haettenschweiler', sans-serif;
  ;
}
</style>
