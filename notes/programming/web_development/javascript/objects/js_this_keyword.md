# The 'this' keyword

In other programming languages, `this` commonly refers to the current object instance inside of a class method. When an object calls a class method, `this` will refer to the property values of the current object instance.

In [JavaScript](../basics/javascript.md), `this` refers to the context of a [function](../basics/js_functions.md) invocation (how a function is executed). There are four types of function invocation in JavaScript:

1. function invocation
2. method invocation
3. constructor invocation
4. indirect invocation

Each type defines the context differently, causing `this` to behave different.

## Function invocation

A function invocation happens every time a normal function gets called.

```js
function add(a, b) {
	return a + b;
}

add(10, 5);  // This is a function invocation
```

In a function invocation, `this` refers to the **global object**. The global object is determined by the execution environment. In a browser, the the global object is the `window` object.

```js
function add(a, b) {
	const sum = a + b;
	this === window;  // true
	this.mySum = sum;
	return sum;
}

add(10, 5);  // 15
window.mySum;  // 15
```

When the `add()` function gets invoked, the value of `this` is set to `window` (the global object in browsers) and any property change made using `this` will be added to `window`.

The same thing happens, when `this` is used outside of functions, in global [scope](../basics/js_scope.md).

```js
this === window;  // true

function test() {
	this === window;  // true
}
```

### Function invocation in strict mode

When using [strict mode](../basics/js_strict_mode.md), the value of `this` in a function invocation will be `undefined` instead of the global object.

```js
function test() {
	"use strict";
	
	this === window;  // false
	this === undefined;  // true
}
```

This does not only apply to the current scope, but also to all inner scopes.

```js
function calculate(a, b) {
	"use strict";

	this === undefined;  // true
	function add(a, b) {
		this === undefined;  // true
		return a + b;
	}

	return add(a, b);
}
```

## Method invocation

A method is a function stored in a property of an [object](js_objects.md). A method invocation happens when a method is called using an object property accessor.

```js
const person = {
	name: "John",

	// This is a method
	greet: function() {
		console.log("Hello!");
	}
};

person.greet();  // This is a method invocation
```

In a method invocation, `this` is the object that owns the method.

```js
const player = {
	name: "John",
	level: 1,

	levelUp: function() {
		// 'this' is set to 'player'
		this.level += 1;
	}
};

player.levelUp();
console.log(player.level);  // 2
```

## Constructor invocation

Constructor invocation happens when a [constructor](js_object_constructors.md) function of an object is called using the `new` keyword.

In a constructor invocation, `this` is the new object that will be created by the constructor.

```js
function Player(name, health, level) {
	this.name = name;
	this.health = health;
	this.level = level;
}

Player.prototype.levelUp = function() {
	this.level += 1;
}

// Constructor invocation
const player1 = new Player("John", 100, 1);

// Method invocation
player1.levelUp();
```

## Indirect invocation

Like many other things in JavaScript, functions are a special type of object. They are known as *first-class citizens*, which means they can be assigned to variables, passed as arguments and even returned from other functions.

Because of this, it is possible to define methods on functions, and all functions have some predefined methods attached to them. These predefined methods include `Function.call()` and `Function.apply()`. These methods are used to change the context of `this` on a function invocation.

These two methods basically work the same, the only difference is the arguments they take in.

- `Function.call(thisArg, arg1, arg2, ...)` takes in the first argument `thisArg` as the new context of the invocation and a list of arguments `arg1, arg2, ...` that are passed as arguments to the function.
- `Function.apply(thisArg, [arg1, arg2, ...])` does the same, but takes in the list of arguments as an array `[arg1, arg2, ...]`. Each array item will be passed as argument to the function.

In an indirect invocation, `this` will be the first argument of `Function.call()` or `Function.apply()`.

```js
const dog = { color: "black" };

function printDogColor() {
	console.log(this.color);
}

printDogColor.call(dog);
printDogColor.apply(dog);
```

## 'this' in arrow functions

In contrast to normal functions, arrow functions **don't** create their own execution context. They inherit the context of `this` from their surrounding scope:

- If an arrow function is defined at top level scope or inside a non-arrow function, it will inherit `window` as value for `this`. This even applies when a method on an object prototype is defined as arrow function.
- If an arrow function is defined inside an object method, it will inherit the parent object as value for `this`.
- If an arrow function is defined inside a constructor, the object that will be created by the constructor will be the value for `this`.
- If the context of a normal function is changed using indirect invocation, an arrow function defined inside it will inherit this changed context for its value for `this`.

It is also not possible to change the context of `this` on arrow functions by using indirect invocation.

## Common pitfalls

There are some common pitfalls when it comes to the context of `this`.

### 'this' in inner functions

A common trap with function invocation is thinking that `this` will be the same in an inner function as in its outer function.

```js
const numbers = {
	numberA: 5,
	numberB: 10,
	
	sum: function() {
		console.log(this === numbers); // => true
		function calculate() {
			console.log(this === numbers); // => false

			// 'numberA' and 'numberB' don't exist on the 'window' object
			// Because of this, 'NaN' will be returned
			return this.numberA + this.numberB;
		}
		
		return calculate();  // This is a function invocation, 'this' is not inherited from the method context
	}
};

numbers.sum();  // NaN
```

### Separating a method from its object

JavaScript allows to separate methods from their objects and store them in variables. It's a common mistake to think that these separated functions are still invoked in the context of the original methods.

When calling such an extracted function, it will no longer be executed as method invocation, instead it will be a normal function invocation. Because of this, the context of `this` will change from the method's parent object to the global object.

```js
const user = {
	name: "John",

	greet: function() {
		console.log(`Hello, my name is ${this.name}`);
	}
};

const extractedGreet = user.greet;

// Method invocation
user.greet();  // "Hello, my name is John"

// Function invocation
extractedGreet();  // "Hello, my name is undefined"
```

The same applies when passing methods as parameters to other functions. The method will be separated from its object.

```js
setTimeout(user.greet, 1000);  // "Hello, my name is undefined"
```

### Forgetting 'new' when using constructors

A function is only invoked as a constructor when it's used together with the `new` keyword. But some functions will create a new instance of an object, even if they aren't invoked as constructors.

```js
function Dog(breed, color, age) {
	this.breed = breed;
	this.color = color;
	this.age = age;

	return this;
}

const husky = Dog("Husky", "grey-white", 3);
husky.breed;  // "Husky"
husky.color;  // "grey-white"
husky.age;  // 3

husky === window;  // true
```

In this example, `Dog()` is invoked as function and not as constructor, because of the missing `new` keyword. Because of this, the context of `this` is `window` and thus the function defines these properties on the global `window` object rather than creating a new one. The `husky` variable is simply set to a reference to the `window` object.

A simple way to avoid this mistake is to use [class](js_classes.md) syntax, since enforces to use the `new` keyword on the constructor and will throw an error if it's missing.

### 'this' context of arrow function can't be changed

Arrow functions inherit their context for `this` from their surrounding scope. Once the context is defined, it can't be changed anymore. This can cause problems when defining methods on the prototype using arrow functions.

```js
function Person(name, age) {
	this.name = name;
	this.age = age;
}

// This method is defined at global scope
// Because it's an arrow function, 'this' is inherited as global object
// The context won't change, even if it's invoked as method
Person.prototype.greet = () => {
	console.log(`My name is ${this.name} and I'm ${this.age} years old.`);
}

const person1 = new Person("John", 25);
person1.greet();  // "My name is undefined and I'm undefined years old."
```