<template>
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
const loading = ref(true);

//Fetch data posts
const fetchPosts = async () => {
  const pending = status === "pending";
  loading.value = pending;
  const url = `https://dummyjson.com/posts?limit=${limit}&skip=${
    (currentPage.value - 1) * limit
  }`;
  const { data, error, status } = await useFetch(url, {
    server: false,
  });
  if (data.value && Array.isArray(data.value.posts)) {
    if (data.value.posts.length < limit) {
      loading.value = false;
    }
    posts.value.push(...data.value.posts);
  } else {
    console.error("Unexpected response structure:", data.value);
  }
  if (error.value) {
    console.error("Fetch error:", error.value);
  } else {
    console.log(data.value);
  }
};

//load more
const loadMore = () => {
  currentPage.value += 1;
  fetchPosts();
};

// Initial fetch when the component mounts
onMounted(() => {
  fetchPosts();
});
</script>
