# Strict mode

[JavaScript](javascript.md) has a feature called *strict mode*. This feature can be enabled to tell the JavaScript runtime to use a stricter set of rules and behavior. Certain actions that would otherwise be ignored or would produce problematic behavior will instead throw errors. This can help to write more robust and maintainable code and can make it easier to catch common mistakes.

## Activating strict mode

Strict mode can be set either only for single [functions](js_functions.md) or for an entire file. It can be declared by adding `"use strict";` to the beginning of either a function or file.

Setting strict mode for a function:

```js
function myFunc() {
	"use strict";

	// This function will be in strict mode
}

// Strict mode will not apply outside of the function
```

Setting strict mode for an entire file:

```js
"use strict";

// Everything in this file will be in strict mode
```

## Difference between normal and strict mode

Strict mode enforces stricter rules and errors that would be ignored in normal JavaScript.

### Using undeclared variables

When assigning a value to an undeclared [variable](js_variables.md), normal JavaScript will implicitly declare a new global variable that will be used.

```js
// This will not throw an error
// Instead, a new global variable 'firstname' will be declared implicitly

function myFunc() {
	firstname = "John";
	console.log(firstname);
}

myFunc();
```

Using strict mode in this same scenario will cause the undeclared variable to throw a `ReferenceError`.

```js
// The undeclared variable will cause strict mode to throw a ReferenceError

function myFunc() {
	"use strict";

	firstname = "John";
	console.log(firstname);
}

myFunc();
```

### Duplicate parameter names

Normal JavaScript will allow to set duplicate names for function parameters. In such a case only the last value of the duplicates will be used.

```js
// Duplicate parameter names will only use the last assigned value

function add(num, num) {
	return num + num;
}

// 3 is the last assigned value
// So the function will evaluate 3 + 3
add(2, 3);  // 6
```

Strict mode doesn't allow to use duplicate parameter names. Instead, it will throw a syntax error. In strict mode each parameter is required to have an unique name.

```js
// Strict mode requires unique parameter names
// It will cause this function to throw a SyntaxError

function add(num, num) {
	"use strict";
	return num + num;
}

add(2, 3);
```

### Using reserved future keywords

JavaScript has a list of reserved keywords that will potentially be used for features in the future. Using these words as names for variables or functions may potentially cause issues in the future.

Some examples for future reserved keywords are: `package`, `interface`, `private`, `public`...

Normal JavaScript allows to use these future reserved keywords as variable or function identifiers.

```js
// 'package' is a reserved keyword for potential future use
// Using it as variable name may cause issues in future versions of JavaScript

const package = "Hello world";
console.log(package);
```

Strict mode doesn't allow to use these reserved keywords to ensure compatibility with future versions of JavaScript. Using a reserved keyword as identifier in strict mode will throw a `SyntaxError`.

```js
// Strict mode will throw a SyntaxError for using a reserved keyword as variable name

"use strict";

const package = "Hello world";
console.log(package);
```

### 'this' in function invocations

The content of the [`this` keyword](../objects/js_this_keyword.md) depends on the way a function is invoked. In normal JavaScript, when a function is called using function invocation, `this` will refer to the global [object](../objects/js_objects.md) (`window` in browsers).

```js
// 'this' will refer to the global object in the context of function invocation

function myFunc() {
	console.log(this);  // window
}

myFunc();
```

This can cause issues when using [constructor functions](../objects/js_object_constructors.md) without the `new` keyword, because the properties defined by the constructor would be added to the global object instead of creating a new object. To avoid this, strict mode will set `this` to `undefined` in the context of function invocation.

```js
// Strict mode sets 'this' to 'undefined' in the context of function invocation

function myFunc() {
	"use strict";
	console.log(this);  // undefined
}

myFunc();
```