# Objects

Objects are the only [data type](../basics/js_data_types.md) that is considered "non-primitive". All the other data types can only store a single value.

In contrast, objects can store various data and even more complex entities and structures in a `key/value` relationship.

An object can be created by using curly braces `{}` containing an optional list of *properties*. A property is a `key/value` pair, where the `key` (also known as property name) has to be a `string`, and the `value` can be anything, even a [function](../basics/js_functions.md) or another object.

An empty object is created like this:

```js
const user = {}; // creates an empty object
```

An object with predefined properties is created like this:

```js
const user = {
	name: "John",
	age: 30,

	// property names can also consist of multiple words
	"likes dogs": true,
};
```

## Accessing properties

There are four main ways to access the properties of an object:
- Dot notation
- Bracket notation
- Using [variables](../basics/js_variables.md) as property names
- Object destructuring

### Dot notation

The object's properties are accessed by referencing them after a dot when accessing the object. This is the preferred way of accessing object properties and should be used whenever possible.

```js
const user = {
	name: "John",
	age: 30,
};

console.log(user.name);
console.log(user.age);
```

### Bracket notation

The object's properties are accessed by wrapping the property names in square brackets. This method is mostly used when the property name consists of multiple words.

```js
const user = {
	name: "John",
	age: 30,
	"likes dogs": true,
};

console.log(user["name"]);
console.log(user["age"]);
console.log(user["likes dogs"]);
```

### Using variables

It is possible to use bracket notation together with separate variables which contain the property names.

```js
const propertyName = "likes dogs"

const user = {
	name: "John",
	age: 30,
	"likes dogs": true,
};

console.log(user[propertyName]);
```

### Object destructuring

This method allows to extract the values of specific properties into new variables.

```js
const user = {
	name: "John",
	age: 30,
};

const { name, age } = user;
console.log(name);
console.log(age);
```

## Computed properties

It is possible to create objects with dynamic property names, for example with names that get generated at runtime. These are called computed properties and can be used by using square brackets in the object definition.

```js
const fruit = prompt("Which fruit to buy?", "apple");

const bag = {
	[fruit]: 5,
};

// both bracket and dot notation can be used
console.log(bag.apple);
console.log(bag[fruit]);
```

## Property value shorthand

When creating objects, it is common to use existing variables as values for property names.

```js
function createUser(name, age) {
	return {
		name: name,
		age: age,
	}
}
```

This is a very common pattern. Because of this, there is a special shorthand when creating properties from variables.

```js
function createUser(name, age) {
	return {
		name, // same as name: name
		age,  // same as age: age
	}
}
```

## Property existence check

The special `in` operator allows to check, if an object has a property with a specific name.

```js
const user = {
	name: "John",
	age: 30,
};

console.log("name" in user); // true
console.log("test" in user); // false
```