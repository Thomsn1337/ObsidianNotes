# Factory functions

Factory functions are an alternative way to [constructors](js_object_constructors.md) for creating [objects](js_objects.md). They achieve this by using the principle of **closures**. Factories provide some advantages over constructor functions.

The main argument against constructors is that they look exactly like regular [functions](../basics/js_functions.md). Because of this, it can easily happen to forget the `new` keyword when using constructors, which can cause the program to fail in many different ways.

## Closures

Closures are formed by functions. A closure refers to the combination of a function and the surrounding state (also known as **lexical environment**) in which it was declared.

A closure is created when a child function is declared inside a parent function. The child function has access to all variables declared inside its own [scope](../basics/js_scope.md), but also the ones in its surrounding scope (the parent function) and global variables.

```js
function parent() {
	const parentVar = "Hello from parent";

	function child() {
		const childVar = "Hello from child";

		console.log(parentVar);  // "Hello from parent"
		console.log(childVar);  // "Hello from child"
	}

	child();
}
```

The power of closures comes into play when returning the inner function. Because of the surrounding state of the closure, the returned child function still has access to variables defined in the parent function, even after its scope was closed.

```js
function parent() {
	const parentVar = "Hello from parent";

	function child() {
		const childVar = "Hello from child";

		console.log(parentVar);  // "Hello from parent"
		console.log(childVar);  // "Hello from child"
	}

	return child;
}

const returnedFunc = parent();
returnedFunc();

// "Hello from parent"
// "Hello from child"
```

## Using factory functions

Just like constructors, factory functions serve the purpose to create new objects. But instead of creating new instances of an object using the `new` keyword, they set up and return an object when a function is called.

```js
function createPlayer(name, health) {	
	return { name, health };
}

const player1 = createPlayer("John", 100);
console.log(player1);
/*
{
	name: "John",
	health: 100,
}
*/
```

A drawback of factories is, that methods that are defined inside the factory are assigned directly to the object and not defined on a [prototype](js_object_prototype.md). This can cause memory and performance issues when creating big amounts of objects from a factory.

### Private variables and methods

The power of closures comes in when adding methods and properties to the object, that are commonly known as *private* values. These values are only used inside the object and are not directly exposed to the outside.

```js
function createPlayer(name, health) {
	let level = 1;

	function getLevel() { return level; }
	function levelUp() { level += 1; }

	return { name, health, getLevel, levelUp };
}

const player1 = createPlayer("John", 100);
console.log(player1.getLevel());  // 1

player1.levelUp();
console.log(player1.getLevel());  // 2

console.log(player1);
/*
	{
		name: "John",
		health: 100,
		getLevel: [Function getLevel],
		levelUp: [Function levelUp]
	}
*/
```

In this example, the `level` variable is not a property of the returned object, it can't be directly accessed when interacting with the object. However, it can be accessed indirectly by methods defined inside the factory. The `.getLevel()` and `.levelUp()` methods can access this variable even after the factory function's scope was closed (when the object gets returned). When the factory defines these methods, they each form their own closure, which has access to all the other *private* properties of the factory.

### Inheritance with properties

Even if factories don't use the prototype, there is a way to achieve inheritance using factories. This method uses the principle of **deconstructing objects**.

```js
function createCreature(name, health) {
	let level = 1;
	
	const getLevel = () => level;
	const levelUp = () => level++;
	
	return { name, health, getLevel, levelUp };
}

function createPlayer(name, health) {
	const { levelUp, getLevel } = createCreature(name, health);

	const attackDamage = 5;
	const getDamage = () => attackDamage;

	return { name, health, getLevel, levelUp, getDamage };
}

const player1 = createPlayer("John", 100);
console.log(player1.getDamage());  // 5
console.log(player1.getLevel());  // 1

player1.levelUp();
console.log(player1.getLevel());  // 2
```