<template>
    <header class="shadow-sm bg-white">
        <nav class="container mx-auto p-4 flex justify-between">
            <nuxt-link to="/" class="font-bold">Home</nuxt-link>
            <nuxt-link to="/about">About</nuxt-link>
            <nuxt-link to="/posts" class="btn">Posts</nuxt-link>
        </nav>
    </header>
    <div class="container mx-auto p-4">
        <slot/>
    </div>
</template>

<script setup>
</script>

<style lang="scss" scoped>
    
</style>