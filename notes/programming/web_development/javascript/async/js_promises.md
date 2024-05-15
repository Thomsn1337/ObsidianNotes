# Promises

Promises are another way to handle [asynchronous code](js_async_code.md), which is often used by libraries or frameworks.

A promise is essentially a special type of [object](../objects/js_objects.md), that might produce a value at some point in the future. Lets say we have a [function](../basics/js_functions.md) called `getData` that fetches some data from a server and returns it as an object:

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

## Creating a promise

Since a promise is a special type of object, it can be created using the `new Promise()` constructor.

```js
const myPromise = new Promise((resolve, reject) => {
	// executor function
})
```

This constructor takes in a function called the **executor**. The executor runs automatically when the promise gets created. It contains the code that should eventually produce the result of the promise.

The executor takes in two arguments, `resolve` and `reject`. These are special [callbacks](js_callbacks.md) provided by JavaScript. The executor should call one of these callbacks, depending on the result it obtained:

- `resolve(value)` - This should be called when the job finishes successfully. It will return `value`.
- `reject(error)` - This should be called when the job fails. The `error` will be returned.

The created `promise` object has two special internal properties:

- `state` - The state of the promise. Its value will be `"pending"` as long as the executor still runs. It then will be changed to either `"fulfilled"` when `resolve` is called or `"rejected"` when `reject` is called.
- `result` - The result of the promise. This will initially be `undefined`. It will then be changed to either `value` when `resolve(value)` is called or `error` when `reject(error)` is called.

```js
const myPromise = new Promise((resolve, reject) => {
	let value;
	// some logic to define the value

	if(value) {
		resolve(value);
	} else {
		reject(new Error("..."));
	}
});
```

In the case that the promise gets rejected, the `reject()` callback should return an `Error` object (or an object that inherits from `Error`).

The `state` and `result` properties of a `promise` object are internal properties and are not directly accessible. To access them, the **consumer** methods `.then` and `.catch` can be used.

### then

The `.then` consumer method will be triggered when the promise is resolved (`state` is set to `"fulfilled"`). It takes in a callback function which provides the value of the resolved promise so it can be used in other parts of the program.

```js
const myPromise = new Promise((resolve, reject) => {
	setTimeout(() => resolve("done"), 1000);
});

myPromise.then((value) => {
	console.log(value);
});
```

It can also take in a second, optional callback function which can be used to handle errors returned if the promise is rejected.

```js
const myPromise = new Promise((resolve, reject) => {
	setTimeout(() => resolve("done"), 1000);
});

myPromise.then(
	(value) => console.log(value),
	(error) => console.error(error)
);
```

### catch

The `.catch` consumer method works similarly to `.then`. It is triggered when the promise is rejected (`state` is set to `"rejected"`). It takes in a callback function which provides the error and is used to handle it.

```js
const myPromise = new Promise((resolve, reject) => {
	setTimeout(() => reject(new Error("Something's gone wrong")), 1000);
});

myPromise.catch((error) => {
	console.error(error);
});
```

The `.catch` consumer method is basically a shorthand for using `.then(null, f)`. It is often times preferred to use `.catch` instead of providing a second argument to `.then` to have a clear separation between using the value of the resolved promise and handling any errors that could occur.

### finally

The `.finally` method isn't a consumer method like `.then` and `.catch`. It **always** runs after the promise has been resolved or rejected and is used to perform any kind of cleanup operations (like closing unneeded connections or stopping loading indicators on the page).

```js
const myPromise = new Promise((resolve, reject) => {
	// some logic
});

myPromise.finally(() => {
		// cleanup operation
	});
```

### Consumer method chaining

It is possible to chain `.then`, `.catch` and `.finally` directly together:

```js
const myPromise = new Promise((resolve, reject) => {
	// some logic
});

myPromise
	.then((value) => {
		// use the value of the resolved promise
	})
	.catch((error) => {
		// handle the error of the rejected promise
	})
	.finally(() => {
		// perform any kind of cleanup operation needed
	});
		```