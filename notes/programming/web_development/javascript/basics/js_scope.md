# Scope

Scope is a simple principle that determines the accessibility (or visibility) of [variables](js_variables.md) throughout the program. In [JavaScript](javascript.md), variables can have three different types of scope:

- Block scope
- Function scope
- Global scope

## Block scope

Block scoped variables are only visible **inside** the block of curly braces `{}` in which they were defined, and any of its child blocks.

A new block is defined by anything that uses curly braces `{}`, for example functions, `if` blocks, loops...

```js
{
	let x = 1;

	// ... some logic ...

	// can be accessed here
	console.log(x);
	{
		// can also be used here
		console.log(x);
	}
}
// can NOT be used here
console.log(x); // Throws ReferenceError: x is not defined
```

Block scope **only exists** for variables declared as `let` or `const`. This is the reason why these methods for variable declaration are preferred over `var`.

```js
{
	var x = 1;

	// ... some logic ...

	// can be accessed here
	console.log(x);
}
// can ALSO be accessed here
console.log(x);
```

## Function scope

Each new function declaration creates a new level of scope. Variables defined inside a function are not accessible outside of it. For `let` and `const` this behaves the same like block scope.

```js
function myFunc() {
	// value1 is accessible throughout the entire function
	const value1 = 1;

	if(true) {
		console.log(value1);  // works

		// value2 is only accessible inside the "if" block
		let value2 = 2;
		console.log(value2);  // works
	}

	console.log(value1);  // works
	console.log(value2);  // doesn't work; ReferenceError
}
```

For `var`, variables are accessible for the entire function, ignoring any other blocks.

```js
function myFunc() {
	if(true) {
		var x = 1;
	}

	console.log(x);  // works
}
```

This happens, because at runtime JavaScript will **hoist (move)** all variable declarations to the top of their current scope. Since `var` ignores block scope, it will be moved to the top of the function scope.

## Global scope

Global scope, also known as top-level scope, is outside of any functions or other blocks. Variables defined inside global scope are known as **global variables** and are accessible throughout the entire file.

```js
let x = 1;

function myFunc() {
	console.log(x);  // logs 1
	x = 2;
}

console.log(x);  // logs 2
```