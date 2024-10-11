<script setup>
import { ref, toRefs } from "vue";
const props = defineProps({
  totalResults: Number,
});

const { totalResults } = toRefs(props);

const emit = defineEmits("pageChanged");

const page = ref(1);

const perPage = 10;

const maxVisibleButtons = 5;

const nextPage = () => {
  if (page.value !== Math.ceil(totalResults.value / perPage)) {
    page.value += 1;
    emit("pageChanged", page.value);
  }
};

const backPage = () => {
  if (page.value !== 1) {
    page.value -= 1;
    emit("pageChanged", page.value);
  }
};

const goToPage = (numPage) => {
  page.value = numPage;
  emit("pageChanged", page.value);
};

const startPage = () => {
  if (page.value === 1) {
    return 1;
  }

  if (page.value === Math.ceil(totalResults.value / perPage)) {
    return Math.ceil(totalResults.value / perPage) - maxVisibleButtons + 1;
  }

  return page.value - 1;
};

const pages = () => {
  const range = [];
  for (
    let i = startPage();
    i <=
    Math.min(
      page.value + maxVisibleButtons - 1,
      Math.ceil(totalResults.value / perPage)
    );
    i++
  ) {
    range.push({ name: i });
  }
  return range;
};
</script>

<template>
  <div class="cont">
    <button class="prevButton" @click="backPage"><</button>
    <button
      v-for="item in pages()"
      :key="item.name"
      @click="() => goToPage(item.name)"
      :class="['pageButton', { activeButton: page == item.name }]"
    >
      {{ item.name }}
    </button>
    <button class="nextButton" @click="nextPage">></button>
  </div>
</template>

<style scoped>
.cont {
  display: flex;
  justify-content: center;
  gap: 0.5rem;
}

.activeButton {
  background-color: var(--primary-red);
  color: var(--primary-white);
}

.pageButton {
  width: 2rem;
  height: 2rem;
  border-radius: 50%;
  border-color: transparent;
  cursor: pointer;
}

.prevButton {
  width: 2rem;
  height: 2rem;
  background-color: transparent;
  border-color: transparent;
}

.prevButton:hover {
  background-color: var(--action-gray);
  border-radius: 50%;
  transition: background-color 250ms linear;
  cursor: pointer;
}

.nextButton {
  width: 2rem;
  height: 2rem;
  background-color: transparent;
  border-color: transparent;
}
.nextButton:hover {
  background-color: var(--action-gray);
  border-radius: 50%;
  transition: background-color 250ms linear;
  cursor: pointer;
}
</style>
