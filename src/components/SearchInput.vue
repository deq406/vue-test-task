<script setup>
import { ref } from "vue";
import SearchIcon from "./icons/SearchIcon.vue";

const emit = defineEmits("search");

const input = ref("");

function onClick() {
  if (input.value) emit("search", input.value);
}
</script>

<template>
  <div class="search">
    <button @click="onClick">
      <SearchIcon />
    </button>
    <input placeholder="Search film" v-model="input" @keyup.enter="onClick" />
  </div>
</template>

<style scoped>
.search {
  position: relative;
}

.search input {
  width: 16rem;
  height: 2rem;

  background: #fcfcfc;
  border: 1px solid #aaa;
  border-radius: 0.5rem;
  box-shadow: 0 0 0.25rem #ccc, 0 0.5rem 1rem #ebebeb inset;
}

.search input {
  text-indent: 1rem;
  padding-right: 3rem;
}

input:focus-visible {
  outline: transparent;
}
button {
  transform: scale(0.8);
  position: absolute;
  left: auto;
  right: 0.2rem;
  background-color: transparent;
  border-color: transparent;
  cursor: pointer;
}

button:hover {
  background-color: var(--icon-hover);
  transition: background-color 250ms linear;
  border-radius: 30%;
}
</style>
