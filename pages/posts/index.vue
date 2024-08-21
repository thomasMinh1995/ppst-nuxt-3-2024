<template>
  <SortDropdown @update:sort="handleSortChange" />
  
  <!-- Search input field -->
  <div class="mb-4">
    <input
      v-model="searchQuery"
      @input="handleSearchChange"
      type="text"
      placeholder="Search posts..."
      class="p-5"
    />
  </div>

  <div class="grid grid-cols-4 gap-4">
    <div v-if="loading">Loading....</div>
    <NuxtLink
      v-else
      :to="`/posts/${p.id}`"
      v-for="p in posts"
      :key="p.id"
      class="post-item"
    >
      {{ p.title }}
    </NuxtLink>
  </div>
  
  <div class="flex justify-center py-3">
    <button class="btn" @click="loadMore" :disabled="loading">
      <p>{{ loading ? "pending" : "Load more" }}</p>
    </button>
  </div>
  <NuxtLoadingIndicator />
</template>

<script setup>
definePageMeta({
  layout: "posts",
});

const posts = ref([]);
const limit = 10;
const currentPage = ref(1);
const loading = ref(false);
const sortCriteria = ref("title:asc"); // Default sort criteria
const searchQuery = ref(""); // Search query state

// Fetch data posts
const fetchPosts = async () => {
  loading.value = true; // Set loading to true when fetching begins

  const [field, order] = sortCriteria.value.split(":");
  let url = `https://dummyjson.com/posts?limit=${limit}&skip=${(currentPage.value - 1) * limit}&sortBy=${field}&order=${order}`;

  if (searchQuery.value) {
    url += `&q=${encodeURIComponent(searchQuery.value)}`; // Add search query to URL
  }

  const { data, error } = await useFetch(url, {
    server: false,
  });

  if (error.value) {
    console.error("Fetch error:", error.value);
  } else if (data.value && Array.isArray(data.value.posts)) {
    posts.value.push(...data.value.posts);
    if (data.value.posts.length < limit) {
      loading.value = false; // Set loading to false if fewer posts than limit
    }
  } else {
    console.error("Unexpected response structure:", data.value);
  }
  loading.value = false; // Set loading to false after fetching is complete
};

// Load more posts
const loadMore = () => {
  if (!loading.value) {
    currentPage.value += 1;
    fetchPosts();
  }
};

// Handle sort change
const handleSortChange = (newSort) => {
  sortCriteria.value = newSort;
  currentPage.value = 1; // Reset to first page
  posts.value = []; // Clear current posts
  fetchPosts();
};

// Handle search change
const handleSearchChange = () => {
  currentPage.value = 1; // Reset to first page
  posts.value = []; // Clear current posts
  fetchPosts();
};

// Watch for changes in sort criteria and refetch posts
watch(sortCriteria, (newSort) => {
  handleSortChange(newSort);
});

// Initial fetch when the component mounts
fetchPosts();
</script>
