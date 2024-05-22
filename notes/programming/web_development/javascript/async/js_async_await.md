# Async and Await

When dealing with larger amounts of [asynchronous code](js_async_code.md), it can become quite difficult to follow. Because of this, the `async` and `await` keywords were introduced. They can help writing code that looks cleaner and can be easier to read by making it look more like normal synchronous code.

```js
function getUserById(id) {
	return server.getUsers().then(users => {
		return users.find(user => user.id === id);
	});
}
```

```js
async function getUserById(id) {
	const users = await server.getUsers();
	const user = users.find(user => user.id === id);

	return user;
}
```

These two code blocks do the exact same thing. They request some data from a server, process it and return a [promise](js_promises.md). But the second one looks much more like a normal, synchronous [function](../basics/js_functions.md).

## The async keyword

The `async` keyword is used to declare an asynchronous function. It is required to declare a function being asynchronous to use `await` inside of it.

Declaring a function as `async` does one simple thing: it ensures that a function returns a promise. Returning inside an `async` function is equal to resolving a promise. Likewise, throwing an error is equal to rejecting a promise.

So `async` functions are just syntactical sugar for using promises.

## The await keyword

The `await` keyword can only be used inside `async` functions. It tells the function to wait for an asynchronous action to finish before continuing to execute. It allows to get a value from a promise where normally `.then()` would be used, and to assign this value directly to a variable.

```js
async function getData() {
	const data = await fetch("https://url.com/api");
	const jsonData = await data.json();

	return jsonData;
}
```

## Handling errors

`async` functions are just a different syntax for promises. If a value is returned inside an `async` function, the promise is resolved normally. If an error is thrown inside it, the promise will be rejected.

The same applies for `await`. If the awaited promise resolves normally, `await` will return the value. If it is rejected, `await` will throw an error.

In case that an error is thrown, there are two main ways to handle them:

- `async` functions return a promise, so the `.catch()` method can be used.

```js
getData().catch((error) => {
	// handle the error
})
```

- Having to append `.catch()` to each `async` function call can be avoided by handling errors directly inside the function body using a `try/catch` block.

```js
async function getData() {
	try {
		const data = await fetch("https://url.com/api");
		const jsonData = await data.json();

		return jsonData;
	} catch (error) {
		// error handling logic
	}
}
```

This block will **try** to execute the code inside the `try` block. If an error is thrown, the `catch` block will **catch** it and the handling logic will be executed.