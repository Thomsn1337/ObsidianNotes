# Working with APIs

A crucial part of [web development](../../basics/web_development.md) is the ability to fetch data from a server through an [API](../../../software_design_and_principles/apis.md) to use it on the own website. Luckily, [JavaScript](../basics/javascript.md) provides a way to achieve this.

The *old* way of making a request to an API was using `XMLHttpRequest`. It is supported by all browsers and can still be used, but it's pretty tedious to use:

```js
let request;

if (window.XMLHttpRequest) { // Mozilla, Safari, ...
	request = new XMLHttpRequest();
} else if (window.ActiveXObject) { // IE
	try {
		request = new ActiveXObject('Msxml2.XMLHTTP');
	}
	catch (e) {
		try {
		  request = new ActiveXObject('Microsoft.XMLHTTP');
		}
		catch (e) {}
	}
}

// Open, send.
request.open('GET', 'https://url.com/some/url', true);
request.send(null);
```

Because this method is so tedious to use, it's not recommended anymore, but can still be encountered in legacy codebases.

## Using fetch

Because `XMLHttpRequest` is so tedious to use, developers began to create 3rd-party alternatives to make it much easier to use.

Recently, JavaScript introduced another native way make [HTTP requests](../../http_requests.md) which is called `fetch`.

```js
fetch("https://url.com/api")
	.then((response) => {
		// Successful request
		// Response can be used here
	})
	.catch((error) => {
		// Error during request
		// It will be handled here
	});
```

While the old `XMLHttpRequest` method was [callback](js_callbacks.md)-based, the `fetch` method is basically a [promise](js_promises.md).

### Enabling CORS

By default, the browser will block such requests to outside sources for security reasons. This can be fixed by telling the `fetch` method to create a request in [CORS](../../../software_design_and_principles/cors.md)-mode.

The `fetch` method takes in the URL for the request as first mandatory argument. It can also take in a second optional argument: an object which is used to set different parameters like the request type, headers...

This object can also be used to define the operation mode of the request to CORS.

```js
fetch("https://url.com/api", {
	mode: "cors"
});
```