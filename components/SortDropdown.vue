<template>
  <div class="pb-4">
    <label for="sort-select">Sort By:</label>
    <select id="sort-select" v-model="selectedSort" @change="emitSort">
      <option value="title:asc">Title (Ascending)</option>
      <option value="title:desc">Title (Descending)</option>
      <option value="date:asc">Date (Ascending)</option>
      <option value="date:desc">Date (Descending)</option>
    </select>
  </div>
</template>

<script setup>
import { ref } from "vue";

const emit = defineEmits(["update:sort"]);

const selectedSort = ref("title:asc");

const emitSort = () => {
  emit("update:sort", selectedSort.value);
};
</script>
