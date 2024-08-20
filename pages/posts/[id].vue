<template>
    <div>
        <h1 class="post-detail-title">{{ item.title }}</h1>
        <p>{{ item.body }}</p>
        <div class="flex gap-5">
            <p>like: {{ item.reactions.likes }}</p>
            <p>dislike: {{ item.reactions.dislikes }}</p>
        </div>
        <div class="post-comments">
            <ul>
                <li v-for="comment in itemComments" :key="comment.id">
                    <h4>{{ comment.user.fullName }} - {{ comment.user.username }}</h4>
                    <p>{{ comment.body }}</p>
                </li>
            </ul>
        </div>
        <div class="py-3 flex justify-center">
            <NuxtLink to="/posts" class="btn">Back</NuxtLink>
        </div>
    </div>
</template>

<script setup>
definePageMeta({
    layout: 'posts'
})
const {id} = useRoute().params;
const data = await useFetch(`https://dummyjson.com/posts/${id}`, {
    key: id
})
const item = data.data.value;

'https://dummyjson.com/posts/1/comments'

const  dataComments = await useFetch(`https://dummyjson.com/posts/${id}/comments`, {
    key: id
})
const itemComments = dataComments.data.value.comments

</script>

<style lang="scss" scoped>

</style>