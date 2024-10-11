<script setup>
import axios from "axios";
import MovieCard from "./MovieCard.vue";
import { onMounted, toRefs, watch } from "vue";
import { reactive } from "vue";
import PulseLoader from "vue-spinner/src/PulseLoader.vue";
import SearchResult from "./SearchResult.vue";
import Pagination from "./Pagination.vue";

const props = defineProps({
  searchStr: String,
});

const { searchStr } = toRefs(props);

const state = reactive({
  movies: [],
  isLoading: true,
  totalResults: null,
});

watch(
  () => searchStr.value,
  async (newVal) => {
    state.isLoading = true;
    try {
      const response = await axios.get(
        "https://www.omdbapi.com/?i=tt3896198&apikey=8523cbb8",
        {
          params: {
            s: newVal,
            page: 1,
          },
        }
      );

      state.movies = response.data.Search;

      state.totalResults = response.data.totalResults;
    } catch (err) {
      console.error("Error fetching movies", err);
    } finally {
      state.isLoading = false;
    }
  }
);

onMounted(async () => {
  try {
    const response = await axios.get(
      "https://www.omdbapi.com/?i=tt3896198&apikey=8523cbb8",
      {
        params: {
          s: "Batman",
          page: 1,
        },
      }
    );

    state.movies = response.data.Search;

    state.totalResults = response.data.totalResults;
  } catch (err) {
    console.error("Error fetching movies", err);
  } finally {
    state.isLoading = false;
  }
});

async function onPageChange(page) {
  try {
    state.isLoading = true;
    const response = await axios.get(
      "https://www.omdbapi.com/?i=tt3896198&apikey=8523cbb8",
      {
        params: {
          s: searchStr.value || "Batman",
          page: page,
        },
      }
    );

    state.movies = response.data.Search;
  } catch (err) {
    console.error("Error fetching movies", err);
  } finally {
    state.isLoading = false;
  }
}
</script>

<template>
  <div class="cont">
    <div v-if="state.isLoading" class="loader">
      <PulseLoader />
    </div>
    <div v-else>
      <SearchResult
        :search="{
          searchInput: searchStr || 'Batman',
          totalResults: state.totalResults,
        }"
      />
      <div class="row">
        <MovieCard
          v-for="movie in state.movies"
          :key="movie.imdbID"
          :movieName="movie.Title"
          :year="movie.Year"
          :id="movie.imdbID"
          :type="movie.Type"
          :poster="movie.Poster"
        />
      </div>
    </div>
    <Pagination
      :totalResults="Number(state.totalResults)"
      @pageChanged="onPageChange"
      v-if="state.totalResults"
    />
  </div>
</template>

<style scoped>
.cont {
  margin-top: 2rem;
}

.row {
  display: flex;
  flex-wrap: wrap;
  gap: 2rem;
  justify-content: center;
}

.loader {
  text-align: center;
}
</style>
