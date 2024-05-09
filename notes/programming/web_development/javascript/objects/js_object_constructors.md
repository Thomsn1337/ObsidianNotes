# Object constructors

Objects are a big part of most [JavaScript](../basics/javascript.md) projects. Because of this, it's common to follow an object-oriented design pattern by grouping related values together into their own object.

A simple example can be taken from something like a *Tic-Tac-Toe* game:

```js
// Example one
// Each value has its own variable
const playerOneName = "John";
const playerTwoName = "Anna";
const playerOneMarker = "X";
const playerTwoMarker = "O";

// Example two
// Grouping values into objects
const playerOne = {
	name: "John",
	marker: "X",
};

const playerTwo = {
	name: "Anna",
	marker: "O",
};
```

This way, other parts of the program can be designed around using these objects. This allows for better code scalability and reusability.

```js
function printWinner(player) {
	console.log(`${player.name} wins!`);
}
```

## Constructors

Creating such objects manually (using the Object Literal method) can be quite tedious. Because of this, there are multiple ways to create predefined values dynamically. The first way is by using **object constructors**. These are special [functions](../basics/js_functions.md) used to create objects.

```js
function Player(name, marker) {
	this.name = name;
	this.marker = marker;
}
```

Such a function allows to easily create `Player` objects by calling it with the `new` keyword.

```js
const playerThree = new Player("Steve", "I");
console.log(playerThree.name);
```

Using constructors also allows to attach functions directly to the object.

```js
function Player(name, marker) {
	this.name = name;
	this.marker = marker;
	
	this.sayName = function() {
		console.log(this.name)
	}
}

const player1 = new Player("John", "X");
const player2 = new Player("Anna", "O");

player1.sayName();  // John
player2.sayName();  // Anna
```

It's important to note that each instance of an object created by a constructor function will create its own copies of all the properties defined in the constructor. This can cause different problems, e.g. higher memory usage when higher amounts of objects are created, or methods not being available in the [prototype chain](js_object_prototype.md).