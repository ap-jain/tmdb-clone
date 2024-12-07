<template>
  <div id="app">
    <AppHeader />
    <main class="container">
      <MovieCard />
    </main>
  </div>
</template>

<script>
import AppHeader from './components/AppHeader.vue';
import MovieCard from './components/MovieCard.vue';

export default {
  components: {
    AppHeader,
    MovieCard,
  },
};
</script>

<style>
*
{
  margin: 0;
  padding: 0;
}
#app {
  background-color: #0d253f;
  color: white;
  min-height: 100vh;
}
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}
</style>
