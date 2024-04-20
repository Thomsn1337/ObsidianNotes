# JavaScript functions

Like any other programming language, [JavaScript](javascript.md) allow to declare functions. A function can be thought of like a small bundle of code that can be reused multiple times inside the program. A function can take in parameters and can also return the result of an operation.

Functions can be used for code organization by logically grouping together parts of code which serve a specific task.

There are two ways of declaring functions in JavaScript:

```js
// The "traditional" way

function myFunc(param1, param2) {
	return param1 + param2;
}

console.log(myFunc(1, 2));
```

```js
// Arrow functions

const myFunc = (param1, param2) => {
	return param1 + param2;
}

console.log(myFunc(1, 2));
```