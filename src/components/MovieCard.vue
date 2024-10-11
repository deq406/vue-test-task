<script setup>
defineProps({
  movieName: String,
  year: String,
  id: String,
  type: String,
  poster: String,
});
</script>

<template>
  <div class="movie-card">
    <img class="movie-header" alt="Movie banner" :src="poster" />
    <div class="movie-content">
      <div class="movie-content-header">
        <a href="#">
          <h3 class="movie-title">{{ movieName }}</h3>
        </a>
      </div>
      <div class="movie-info">
        <div class="info-section">
          <label>Year</label>
          <span>{{ year }}</span>
        </div>
        <div class="info-section">
          <label>Id</label>
          <span>{{ id }}</span>
        </div>
        <div class="info-section">
          <label>Type</label>
          <span>{{ type }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
* {
  transition: 300ms;
}

h1,
h2,
h3,
h4,
h5,
p {
  font-weight: 400;
}

a {
  text-decoration: none;
  color: inherit;
}

a:hover {
  color: var(--link-hover);
}

.movie-card {
  background: var(--primary-white);
  box-shadow: 0px 0.5rem 1rem rgba(0, 0, 0, 0.1);
  width: 100%;
  max-width: 20rem;
  margin: 2rem;
  border-radius: 0.5rem;
  display: inline-block;
}

.movie-header {
  padding: 0;
  margin: 0;
  height: 20.5rem;
  width: 100%;
  display: block;
  border-top-left-radius: 0.5rem;
  border-top-right-radius: 0.5rem;
}

.movie-card:hover {
  transform: scale(1.03);
  box-shadow: 0px 1rem 2rem rgba(0, 0, 0, 0.5);
}

.movie-content {
  padding: 1rem 1rem 2rem 1rem;
  margin: 0;
}

.movie-title {
  font-size: 1.5rem;
  margin: 0;
}

.movie-info {
  margin-top: 1rem;
  display: flex;
  flex-direction: column;
}

.info-section {
  text-transform: uppercase;
}

.info-section label {
  display: block;
  color: rgba(0, 0, 0, 0.5);
  font-size: 0.5rem;
}

.info-section span {
  font-weight: 700;
  font-size: 0.7rem;
  line-height: 1.5rem;
}

@media screen and (max-width: 500px) {
  .movie-card {
    width: 95%;
    max-width: 95%;
    margin: 1rem;
    display: block;
  }
}
</style>
