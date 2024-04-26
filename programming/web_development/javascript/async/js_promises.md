# Promises

Promises are another way to handle [asynchronous code](js_async_code.md), which is often used by libraries or frameworks.

A promise is essentially a special type of [object](js_objects.md), that might produce a value at some point in the future. Lets say we have a [function](js_functions.md) called `getData` that fetches some data from a server and returns it as an object:

```js
function getData() {
	// fetch data from server
	// return data as object
	return data;
}
```

The data fetch takes some time, but the program doesn't know that and thinks that `getData` is a normal synchronous function.

```js
const data = getData();
const parameter = data["parameter"]; // undefined
```

Trying to extract a piece from the fetched data would return `undefined`, because the `getData` function will most likely still be fetching at that point.

Promises can be used to solve this issue. They allow to define what should happen when an asynchronous action has completed:

```js
const myData = getData(); // refactored to return a promise

// .then() gets executed when the promise is resolved
// It then executes the provided callback function
myData.then((data) => { 
	const parameter = data["parameter"];
});
```