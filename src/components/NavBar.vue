<script setup>
import ProfileIcon from "./icons/ProfileIcon.vue";
import SearchInput from "./SearchInput.vue";
const userName = "Alexander Borisenko";

const emit = defineEmits("search");

function onSearch(searchStr) {
  emit("search", searchStr);
}
</script>

<template>
  <navbar class="cont">
    <h3>Movie Catalog</h3>
    <SearchInput @search="onSearch" />
    <div class="profile__cont">
      <ProfileIcon />
      <div>
        {{ userName }}
      </div>
    </div>
  </navbar>
</template>

<style scoped>
.cont {
  display: flex;
  justify-content: space-around;
  align-items: center;
  min-height: 4rem;
  background-color: var(--primary-red);
  flex-wrap: wrap;
}

h3 {
  margin: 0;
  color: var(--primary-white);
}

.profile__cont {
  display: flex;
  gap: 0.4rem;
  color: var(--primary-white);
}

@media screen and (max-width: 600px) {
  input {
    min-width: 15rem;
  }
  .cont {
    flex-direction: column;
    gap: 1rem;
  }
}
</style>
