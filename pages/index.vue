<template>
    <div>
        <h1 class="text-center">This is an home page</h1>
        <div v-for="quote in quotesList" class="grid grid-cols-1">
            <div class="flex justify-center flex-col items-center border-2 border-solid border-slate-400 rounded-md my-4">
                <p class="italic pb-3 text-base text-center">{{ quote.quote }}</p>
                <p class="text-base">{{ quote.author }}</p>
            </div>
        </div>
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

    const { data: quotes, error } = await useFetch('https://dummyjson.com/quotes');

    const quotesList = quotes.value?.quotes;

    console.log('data', quotes.value?.quotes)
</script>