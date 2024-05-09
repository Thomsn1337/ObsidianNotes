# The object prototype

All [objects in JavaScript](js_objects.md) have a prototype. The prototype is another object, that the original one *inherits* from. This means, that the original object does not only have access to its own properties and methods, but also to the ones of the prototype.

The prototype of an object can be accessed using the `Object.getPrototypeOf()` function.

```js
function Player(name, level) {
	this.name = name;
	this.level = level
}

const player1 = new Player("John", 1);

Object.getPrototypeOf(player1) === Player.prototype;  // true
```

It is possible to define methods on the prototype of the object.

```js
Player.prototype.levelUp = function() {
	this.level += 1;
}

player1.levelUp();

console.log(player1.level);  // 2
```

## Prototypal inheritance

As mentioned before, the prototype can be thought of as a template object that other object instances can *inherit* their properties from. *Inheriting* simply means that objects can access anything that was defined on their prototype. 

Properties and methods that are defined on the prototype are common among all of its object instances. If an object calls one of these methods, it will access its definition on the prototype. If they would instead be defined on the [constructor](js_object_constructors.md), each object instance would create its own copy of the common methods and properties, which will cause higher memory usage.

Since prototypes are objects aswell, they also have their own prototypes, which they inherit some properties from.

```js
Object.getPrototypeOf(Player.prototype) === Object.prototype;  // true

player1.toString(); // Method coming from Object.prototype
```

This principle is known as the **prototype chain**. If a property or method is not defined on an object directly, it will search for it on its prototype. If it can't find it there, it will go up the chain, until it eventually finds it.

It is possible to check, which properties belong to which prototype by using the `.hasOwnProperty()` function.

```js
player1.hasOwnProperty("toString");  // false
Object.prototype.hasOwnProperty("toString");  // true
```

The `hasOwnProperty()` function is another example for inheritance. Each object inherits it from `Object.prototype`.

### The prototype chain

As mentioned above, the prototype chain is simply a chain of prototypes, which inherit properties from each other. If an object calls a property, it will go up the chain, until it can find it.

However, this chain does not go on forever. `Object.prototype` is the base prototype that each object will inherit from by default. All the basic object properties (like `toString()`, `hasOwnProperty()`, etc.) are defined here. It doesn't have a prototype itself.

```js
Object.getPrototypeOf(Object.prototype);  // null
```

### Setting prototypes

Similar to using `Object.getPrototypeOf()` to get information about an objects' prototype, it is possible to define the prototype of an object by using the `Object.setPrototypeOf()` function.

```js
function Creature(name, health) {
	this.name = name;
	this.health = health;
}

Creature.prototype.attack = function() {
	console.log(`${this.name} attacked!`);
}

function Player(name, health, level) {
	this.name = name;
	this.health = health;
	this.level = level;
}

Player.prototype.levelUp = function() {
	this.level += 1;
}

// Setting the prototype of 'Player' to 'Creature'
Object.setPrototypeOf(Player.prototype, Creature.prototype);

const player1 = new Player("John", 100, 1);
player1.attack(); // "John attacks!"
player1.levelUp();

Player.prototype.hasOwnProperty("levelUp");  // true
Player.prototype.hasOwnProperty("attack");  // false

Creature.prototype.hasOwnProperty("attack");  // true
```

In this example, `Player` inherits the `attacK()` method from `Creature`. By setting the prototype of `Player` to `Creature`, all `Player` objects are not only able to access their own properties, but also the ones of `Creature`.