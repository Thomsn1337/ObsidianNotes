# Events in JavaScript

Events are actions that happen on a web page, such as key presses or mouse clicks. [JavaScript](javascript.md) allows to listen for such events and to react to them, for example by running a [function](js_functions.md).

There are three main ways to execute code when an event occurs:
- Assign a function to the corresponding event [attribute](html_attributes.md) on the [HTML element](html_elements_tags.md) directly (for example `onclick`).
- Set the corresponding properties on a selected [DOM node](js_dom_manipulation.md).
- Attach event listeners to a selected DOM node.

## Method 1

```html
<button onclick="console.log('Clicked!')">Click me</button>
```

This method is the least preferred, because the HTML file gets cluttered with JavaScript. This method also only allows to run a single function per element.

## Method 2

```html
<!-- index.html -->

<button id="btn">Click me</button>
```

```js
// index.js

const button = document.querySelector("#btn");
btn.onclick = () => console.log("Clicked");
```

With this method, the JavaScript code gets moved out of the HTML file, but each DOM node still has a single `onclick` property.

## Method 3

```html
<!-- index.html -->

<button id="btn">Click me</button>
```

```js
// index.js

const button = document.querySelector("#btn");
button.addEventListener("click", () => {
	console.log("clicked");
});
```

This is the preferred method, because it allows for multiple listeners per node and is much more flexible.

The `element.addEventListener()` function takes in two required arguments:
- The event to listen for
- A function to execute when the event occurs

This function is called a [callback function](js_callbacks.md). This function can be defined somewhere else in the code, or directly as a parameter, as in the above example.

The callback function can also take in a parameter, but doesn't have to. If it takes in a parameter, the event listener passes the event to the function. This allows to gather more information about the event or to call one of its methods: 

```js
const button = document.querySelector("#btn");
button.addEventListener("click", (e) => {
	// Prints information about the event to the console
	console.log(e);

	// Prevents the default action that would happen when the event occurs
	e.preventDefault();
});
```

Some useful events that can be listened for include:
- `click` - the element is clicked
- `keydown` - a keypress is registered
- `keyup` - the keypress stopped
- `mouseenter` - the cursor entered the element
- `mouseleave` - the cursor left the element

A more complete list of events can be found [here](https://www.w3schools.com/jsref/dom_obj_event.asp).