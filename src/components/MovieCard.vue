<template>
  <div class="movie-card">
    <img :src="movie.poster" alt="Movie Poster" class="poster" />
    <div class="details">
      <h1>{{ movie.title }} ({{ movie.year }})</h1>
      <p>{{ movie.releaseDate }} • {{ movie.genre }} • {{ movie.runtime }}</p>
      <div class="score-container">
        <div class="score">
          <span>{{ movie.rating }}%</span>
        </div>
        <span>User Score</span>
      </div>
      <br />
      <div class="buttons-container">
        <button class="trailer-btn">list</button>
        <button class="trailer-btn">like</button>
        <button class="trailer-btn">save</button>
        <button class="trailer-btn play-trailer">Play Trailer</button>
      </div>
      <br /><br />
      <h2>Overview</h2>
      <p>{{ movie.plot }}</p>
      <br /><br />
      <table style="width: 100%">
        <tr>
          <td>{{ movie.director }}</td>
        </tr>
        <tr>
          <td>Director</td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
import { onMounted, ref } from "vue";
import "../assets/movie-card.css";

export default {
  setup() {
    const movie = ref({
      title: "",
      year: "",
      releaseDate: "",
      genre: "",
      runtime: "",
      rating: "",
      poster: "",
      plot: "",
      director: "",
    });

    onMounted(() => {
      const apiUrl = "http://www.omdbapi.com/?i=tt3896198&apikey=d2132124";

      fetch(apiUrl)
        .then((response) => response.json())
        .then((data) => {
          movie.value = {
            title: data.Title,
            year: data.Year,
            releaseDate: data.Released,
            genre: data.Genre,
            runtime: data.Runtime,
            rating: data.Ratings[0]?.Value || "N/A",
            poster: data.Poster,
            plot: data.Plot,
            director: data.Director,
          };
          console.log(data);
        })
        .catch((error) => {
          console.error("Error fetching data:", error);
        });
    });

    return {
      movie,
    };
  },
};
</script>

<style scoped></style>
