<template>
  <nav class="navbar">
    <div class="container">
      <!-- Logo Section -->
      <div class="navbar-header">
        <a class="navbar-brand" href="#">TMDB</a>
      </div>

      <button class="navbar-toggle" @click="toggleMenu">☰</button>
      
      <ul class="nav" :class="{ 'show-menu': isMenuOpen }">
        <li class="nav-item"><a href="#">Movies</a></li>
        <li class="nav-item"><a href="#">TV Shows</a></li>
        <li class="nav-item"><a href="#">People</a></li>
        <li class="nav-item"><a href="#">More</a></li>
      </ul>

      <ul class="nav navbar-right actions" :class="{ 'show-menu': isMenuOpen }">
        <i class="fas fa-plus"></i>
        <li class="nav-item"><a href="#">EN</a></li>
        <li class="nav-item"><a href="#">Login</a></li>
        <li class="nav-item"><a href="#">Join TMDB</a></li>
        <i class="fas fa-search"></i>
      </ul>
    </div>
  </nav>

  <!-- Secondary Header -->
  <div class="second_header">
    <nav>
      <a href="#" class="dropdown-toggle">Overview&nbsp;<i class="fas fa-angle-down"></i></a>
      <a href="#" class="dropdown-toggle">Media&nbsp;<i class="fas fa-angle-down"></i></a>
      <a href="#" class="dropdown-toggle">Fandom&nbsp;<i class="fas fa-angle-down"></i></a>
      <a href="#" class="dropdown-toggle">More&nbsp;<i class="fas fa-angle-down"></i></a>
    </nav>
  </div>
</template>

<script>
import "../assets/navbar.css";

export default {
  data() {
    return {
      isMenuOpen: false,
    };
  },
  methods: {
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen;
    },
  },
};
</script>

<style scoped>
/* Navbar Base Styling */

</style>
