# Getters and setters

[Objects](js_objects.md) can have two different types of properties, **data properties** and **accessor properties**. Data properties are the commonly used ones. They are used to store some type of data inside an object.

Accessor properties don't store any data by themselves. They define a function that will be called when the property gets called or written to. They are commonly used to execute specific code when getting or setting a value, e.g. performing data validation.

## Using getters and setters

Accessor properties are categorized into `getter` and `setter` methods. They can be defined by using `get` or `set` on an object property.

```js
const myObj = {
	get fullName() {
		// this will be executed when reading 'myObj.fullName'
	},

	set fullName() {
		// this will be executed when writing to 'myObj.fullName'
	}
}
```

Getters are executed when reading a property value, setters are executed when writing to it.

A common usecase for a getter can be to compute property values on the fly based on other properties of the object. This way the getter value will update automatically when other properties, which it depends on, change.

```js
const person = {
	firstName: "John",
	lastName: "Smith",

	get fullName() {
		return `${this.firstName} ${this.lastName}`;
	}
};

console.log(person.fullName);  // "John Smith"

person.firstName = "Matthew";
console.log(person.fullName);  // "Matthew Smith"
```

Setters are used to control how values are assigned to an objects' property. They can be used to perform data validation or to trigger specific actions when setting a property.

```js
const person = {
	firstName: "John",
	lastName: "Smith",
	age: 27,

	set age(newAge) {
		if(newAge >= 0 && newAge <= 100) {
			this.age = newAge;
		} else {
			console.error("Invalid value provided");
		}
	}
};

person.age = 30;  // Valid assignment
person.age = 110;  // Invalid assignment, logs error message
```