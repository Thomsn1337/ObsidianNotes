# Callbacks

A callback function is a [function](javascript_functions.md) gets passed to another function as one of its parameters. This inner callback function will then be invoked (executed) by the outer function at some point to complete some kind of action. Callbacks are mostly used in the context of [asynchronous code](javascript_async_code.md)

```js
function handleClick() {
	// some logic
}

// This event can occur at any time, its asynchronous
myButton.addEventListener("click", handleClick)
```

Callbacks are not exclusive to asynchronous code, synchronous functions can also accept callback functions as parameters:

```js
const myArray = ["one", "two", "three"];

// This is a synchronous function which takes a callback function as parameter
myArray.forEach((item) => {
	console.log(item)
});
```