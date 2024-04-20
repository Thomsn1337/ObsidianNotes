# JavaScript

JavaScript is a versatile and widely used programming language. It is mostly used to add interactivity and dynamic content to webpages. JavaScript gives you the ability to dynamically manipulate both the [html](html.md) content and the [css](css.md) styles on a webpage. The main method to achieve this is by listening for specific events (e.g. a click on a button). Triggering such an event causes a specific part of the JavaScript code to be executed. It is also the main tool to connect the front-end with the server-side logic of a web app.

## Running JavaScript

There are multiple ways to run JavaScript code. One way is running it in the browser. This can be done by using one of these methods:

- Writing code inside of a `script` tag in the HTML file.

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>Page Title</title>
	</head>

	<body>
		<script>
			// Your JavaScript goes here!
			console.log("Hello, World!")
		</script>
	</body>
</html>
```


- Importing a JavaScript file in the HTML code. This can be done by using the `src` attribute of the `script` tag. This method is recommended as soon as the JavaScript part of a project gets bigger.

```html
<!-- index.html -->

<script src="path/to/index.js"></script>
```

```js
//index.js

console.log("Hello, world!")
```