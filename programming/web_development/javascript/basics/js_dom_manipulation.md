# DOM manipulation in JavaScript

[JavaScript](javascript.md) allows to interact with [the DOM](html_dom.md). It allows to select specific nodes from the DOM by using the `document.querySelector()` function.

This function can be used to select a specific DOM node by providing a selector as its parameter. This selector can consist of a combination of [CSS selectors](css.md#selectors) and [relationship combinators](css_combinators.md).

```html
<!-- index.html -->

<div id="container">
	<div class="display"></div>
	<div class="controls"></div>
</div>
```

```js
// index.js

const container = document.querySelector("#container");

const display = document.querySelector("#container .display");
```

A selected node owns special properties which contain relational selectors. These can also be used to select nodes.

```js
const container = document.querySelector("#container");

const display = container.firstElementChild;
const controls = display.nextElementSibling;
```

## DOM methods

When a HTML document gets parsed by the browser, it is converted into the DOM. For each element in the document, a new node in the DOM is created. These nodes are basically JavaScript objects which have different properties and methods attached to them. These properties and methods can be used to interact with the nodes and to manipulate the DOM.

### Query selectors

There are two types of query selectors which can be used to select child nodes from a specific node in the DOM:

```js
element.querySelector(selector);
```

This function returns a reference to the first match of *selector*.

```js
element.querySelectorAll(selector);
```

This function returns a *NodeList*, a special type of array containing references to all matches of *selector*.

### Creating elements

JavaScript allows to create new elements in the DOM.

```js
const div = document.createElement("div");
```

This method **doesn't** append the newly created element to the DOM, it only creates it in memory.

### Appending elements

There are two methods to append a newly created element to the DOM:

```js
parent.appendChild(child);
```

This function appends *child* as the last child of *parent*.

```js
parent.insertBefore(newNode, referenceNode);
```

This function inserts *newNode* into *parent* before *referenceNode*.

### Removing elements

There is a method to remove a child node from a parent node:

```js
parent.removeChild(child);
```

### Editing node attributes

When creating new elements or selecting them from the DOM, it is possible to edit the element's attributes:

```js
const div = document.createElement("div");

// Add or change the ID of the element
div.id = "my-id";

// Add a new class
div.classList.add("new-class");

// Remove a class
div.classList.remove("old-class");

// Toggle a class
// If it's not present, add it
// If it's present, remove it
div.classList.toggle("active");

// Change the text content of the element
div.textContent = "Hello world";

// Render a new HTML element inside the element
div.innerHTML = "<button>Click me</button>";
```