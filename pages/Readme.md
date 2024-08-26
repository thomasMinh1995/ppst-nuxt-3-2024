## How to call api quotes from the dummyjson:

# 1st: using destructuring
// const { data: quotes, error } = await useFetch('https://dummyjson.com/quotes', {
//     server: false
// });
// console.log('data._object', quotes.value.quotes)
// console.log('data._object', quotes._value)


# 2nd: assign variable
// const data = await useFetch('https://dummyjson.com/quotes', {
//     server: false
// });
// const item = data.data.value;
// console.log('hello', item)