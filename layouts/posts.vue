<template>
    <header class="shadow-sm bg-white">
        <nav class="container mx-auto p-4 flex justify-between">
            <nuxt-link to="/" class="font-bold">Home</nuxt-link>
        </nav>
    </header>
    <div class="container mx-auto p-4">
        <slot/>
    </div>
</template>

<script>
export default {
    setup () {
        

        return {}
    }
}
</script>

<style lang="scss" scoped>

</style>