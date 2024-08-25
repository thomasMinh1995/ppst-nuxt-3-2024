<template>
    <div>
        <h1>This is an home page</h1>
    </div>
</template>

<script setup>
// const { data: quotes, error } = await useFetch('https://dummyjson.com/quotes', {
//     server: false
// });

// console.log('data._object', quotes.value.quotes)
// console.log('data._object', quotes._value)


// const data = await useFetch('https://dummyjson.com/quotes', {
//     server: false
// });

// const item = data.data.value;
// console.log('hello', item)

// export default {
//     async setup() {
        const { data, error } = await useFetch('https://dummyjson.com/quotes');

        console.log('data', data.value?.quotes)
        // return { quotes: data.value?.quotes, error: error.value };
//     }
// }
</script>