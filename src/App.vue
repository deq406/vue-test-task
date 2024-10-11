<script setup>
import "./assets/base.css";
import { ref } from "vue";
import NavBar from "./components/NavBar.vue";
import MovieGrid from "./components/MovieGrid.vue";
const input = ref("");

function onSearch(searchStr) {
  input.value = searchStr;
}
</script>

<template>
  <NavBar @search="onSearch" />
  <MovieGrid :searchStr="input" />
</template>
