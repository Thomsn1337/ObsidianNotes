# Classes

In [JavaScript](../basics/javascript.md) classes do not work the same way as in other [object-oriented](../../../basics/object_oriented_programming.md) languages. They still serve the purpose of creating [objects](js_objects.md), but are just a different syntax for using [constructors](js_object_constructors.md) and [prototypes](js_object_prototype.md).

```js
class Person {
	constructor(firstName, lastName, age) {
		this.firstName = firstName;
		this.lastName = lastName;
		this.age = age;
	}

	greet() {
		console.log(`Hello, my name is ${this.firstName} ${this.lastName}`);
	}
}

const person1 = new Person("John", "Smith", 25);
person1.greet();
```

## What is a class?

A class in JavaScript is a special kind of function used to simplify constructors and prototypes. It creates a function named after the class (in the above example `Person`). The code of this function is taken from the `constructor()` method. Properties and methods defined outside the `constructor()` will be stored on the objects' prototype (in the above example `Person.prototype`).

```js
class Person {
	constructor(name) {
		this.name = name;
	}

	greet() {
		console.log(`Hi, my name is ${this.name}`);
	}
}

// The class is a function
console.log(typeof Person);  // function

// It is the constructor method
console.log(Person === Person.prototype.constructor);

// Methods defined inside the class are stored on the prototype
console.log(Object.getOwnPropertyNames(User.prototype));  // constructor, greet
```

The `class` syntax is often marked off as *syntactic sugar* that is only designed to make the concept of constructors and prototypes easier to read and doesn't introduce anything new. But classes introduce some notable differences to constructors and prototypes:

- Functions created by a class are labelled with a special internal property called `[[IsClassConstructor]]: true`. JavaScript checks for this property in a variety of places, e.g. constructors are required to be called with `new`.

```js
class Person {
	constructor() {}
}

const john = User();  // TypeError: Class constructor Person cannot be invoked without 'new'
```

- Class methods are *non-enumerable*. This means that when iterating over an object using a `for...in` loop, the methods, which the object has access to, are ignored.
- Classes use [strict mode](../basics/js_strict_mode.md) by default, meaning that all the methods and properties defined inside a class construct are automatically in strict mode.

## Getters and setters

Just like in normal objects, it is possible to define [getters and setters](js_getters_setters.md) on a class.

```js
class Person {
	constructor(name, age) {
	    this._name = name;
	    this._age = age;
	}

	get age() {
	    return this._age;
	}

	set age(val) {
	    if (val <= 0 || val >= 110) {
		console.error("Invalid age value");
		return;
		}
		this._age = val;
	}
}

const person = new Person("John", 24);
console.log(person.age);

person.age = 120; // Invalid age value
```

## Class fields

Class fields allow to add any type of property to a class, not just methods. Such properties can be created using either simple assignments or more complex expressions and function calls.

```js
class User {
	name = "John";
	id = Date.now();
}

console.log(new User().name);
console.log(new User().id);
```

There is an important difference between class fields and methods:

- Methods are defined **on the prototype** of the object.
- Class fields are defined **individually on each object instance**.

```js
class User {
	name = "John";
}

const user = new User();

console.log(user.name);  // John
console.log(User.prototype.name);  // undefined
```

### Private properties

Classes allow to define private properties which are only accessible from within the class itself. Trying to access a private property from outside the class will cause an error. Private properties are useful to hide away complex internal logic of a class and only expose needed functions, which is a common pattern in [encapsulation](../../../basics/encapsulation.md).

Private properties can be defined by prefixing class field properties or methods with a hash sign `#`. Other than normal properties, they have to be explicitly defined before they can be accessed.

```js
class Rectangle {
	#width;
	#height;

	constructor(width, height) {
		this.#width = width;  // Ok
		this.#height = height;  // Ok

		this.#area = width * height;  // Error
	}
}
```

### Binding methods with class fields

When passing object methods around as function parameters, a common problem with the dynamic behavior of the [`this` keyword](js_this_keyword.md) can occur. When an object method is passed as function parameter, `this` will no longer be a reference to the object.

```js
class Person {
	constructor(name) {
		this.name = name;
	}

	greet() {
		console.log(this.name);
	}
}

const person = new Person("John");

setTimeout(person.greet, 1000);  // undefined
```

For classical object constructors and prototypes there are two approaches to fixing this problem:

- Passing a wrapper function that will explicitly call the method.

```js
setTimeout(() => person.greet(), 1000);
```

- Binding the method to the object, e.g. by defining it in the constructor.

Classes provide another way to fix this problem, which uses fields and arrow functions.

```js
class Person {
	constructor(name) {
		this.name = name;
	}

	greet = () => {
		console.log(this.name);
	}
}
```

In this example, `greet` is defined as a class field property instead of a method. The content of the field property is an arrow function. Because field properties will be defined for each instance of an object individually, the context of `this` will be bound to the instance. Since arrow functions can't change their context of `this` after definition, the function will be bound to the object instance and can be passed around as parameter.

## Inheritance

The `extends` keyword can be used in class declarations to create a class which inherits properties from another constructor. This can be either another class or a constructor function.

```js
class Creature {
	constructor(name, health) {
		this.name = name;
		this.health = health;
	}

	attack() {
		console.log(`${this.name} attacked!`);
	}
}

class Player extends Creature {
	constructor(name, health, level) {
		super(name, health);  // Calls the parent class' constructor
		this.level = level;
	}

	levelUp() {
		this.level += 1;
	}
}

const player = new Player("John", 100, 1);
player.attack();  // "John attacks!"
player.levelUp();

Player.prototype.hasOwnProperty("levelUp");  // true
Player.prototype.hasOwnProperty("attack");  // false

Creature.prototype.hasOwnProperty("attack");  // true
```

The child class has to call `super()` in its constructor before it can access its own `this`. The `super()` function calls the constructor of the parent class, which is necessary to set up its own state and initializing properties and method so they are accessible for the child class. This also ensures proper establishment of the inheritance chain.

The `super` keyword can be used to access properties and methods defined in the parent class.

```js
class Creature {
	constructor(name, health) {
		this.name = name;
		this.health = health;
	}

	attack() {
		console.log(`${this.name} attacked!`);
	}
}

class Player extends Creature {
	constructor(name, health, weapon) {
		super(name, health);  // Calls the parent class' constructor
		this.weapon = weapon;
	}

	attack() {
		super.attack();
		console.log(`${this.name} used ${this.weapon}`);
	}
}

const player = new Player("John", 100, "Axe");
player.attack();

// John attacked!
// John used Axe
```

## Static properties and methods

Static properties and methods belong to the class itself rather than to an instance of the class. This means that they can be accessed directly on the class without the need of creating an instance first.

They can be declared by prefixing any property of a class with the `static` keyword.

```js
class Animal {
	static type = "Animal";

	static speak() {
		console.log("Generic sound");
	}
}

class Dog extends Animal {
	static speak() {
		console.log("Woof");
	}
}

console.log(Animal.type);  // Animal
console.log(Dog.type);  // Animal

Animal.speak();  // Generic sound
Dog.speak();  // Woof
```

Static properties are commonly used for utility functions that the class will provide, like special functions to create or clone instances. They are also useful to define properties that should only once per class and not on each instance. 