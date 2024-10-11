<script setup>
defineProps({
  search: {
    searchInput: String,
    totalResults: Number,
  },
});
</script>

<template>
  <p v-if="!search.totalResults" class="title">No results</p>
  <p v-else class="title">
    You searched for: {{ search.searchInput }},
    {{ search.totalResults }} results found
  </p>
</template>

<style scoped>
.title {
  font-weight: 500;
  font-size: 1.5rem;
  text-align: center;
}
</style>
