<template>
  <div class="movie-card" >
    <!-- Search bar -->
    <div class="search-container">
      <input
        v-model="searchText"
        type="text"
        placeholder="Search for a movie..."
        class="search-input"
        @keyup.enter="searchMovie" 
        />
      <button @click="searchMovie" class="search-btn">Search</button>
    </div>

    <!-- Loader while searching -->
    <div v-if="loading" class="loader-container">
      <div class="loader"></div> <!-- This is the loader animation -->
    </div>

    <!-- Movie details section -->
    <div v-if="movie.title && !loading" class="main-div">
      <img :src="movie.poster" alt="Movie Poster" class="poster" />
      <div class="details">
        <h1>{{ movie.title }} ({{ movie.year }})</h1>
        <p>{{ movie.releaseDate }} • {{ movie.genre }} • {{ movie.runtime }}</p>
        <div class="score-container">
          <div class="score">
            <span>{{ movie.rating }}</span>
          </div>
          <span>TMDB Rating</span>
        </div>
        <br />
        <div class="buttons-container">
          <button class="trailer-btn"> <i class="fas fa-list"></i>&nbsp;list</button>
          <button class="trailer-btn"> <i class="fas fa-thumbs-up"></i>&nbsp;like</button>
          <button class="trailer-btn"> <i class="fas fa-save"></i>&nbsp;save</button>
          <button class="trailer-btn play-trailer"><i class="fas fa-play"></i>&nbsp;Play Trailer</button>
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

    <!-- Show error message if movie is not found -->
    <div v-else-if = "!loading">
      <p>No movie found. Please try another search.</p>
    </div>
  </div>
</template>


<script>
import { onMounted, ref } from "vue";
import "../assets/movie-card.css";

export default {
  setup() {
    const searchText = ref(""); // Search query
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
    const loading = ref(false); // Loading state to show loader during fetch

    // Function to search movie
    const searchMovie = () => {
      loading.value = true; // Set loading to true when search begins

      const apiUrl = `http://www.omdbapi.com/?t=${searchText.value}&apikey=d2132124`;

      fetch(apiUrl)
        .then((response) => response.json())
        .then((data) => {
          if (data.Response === "True") {
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
          } else {
            movie.value = {}; // Clear the movie details if no result is found
          }
        })
        .catch((error) => {
          console.error("Error fetching data:", error);
          movie.value = {}; // Clear the movie details on error
        })
        .finally(() => {
          // Set loading to false after 2 seconds
          setTimeout(() => {
            loading.value = false; // Hide loader after 2 seconds
          }, 2000); // 2000ms = 2 seconds
        });
    };

    // Initially fetch a movie (example movie)
    onMounted(() => {
      searchText.value = "Guardians of the Galaxy"; // Default search text
      searchMovie(); // Fetch the movie on mount
    });

    return {
      searchText,
      movie,
      loading,
      searchMovie,
    };
  },
};
</script>



<style scoped></style>
