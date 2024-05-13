# Webpack

Webpack is a powerful tool in the [web development](../../basics/web_development.md) ecosystem. It is mostly known for its [bundling](bundling.md) capabilities. It takes in a [JavaScript](../basics/javascript.md) file, analyzes its structure and creates a graph of all the dependencies of this entry file and bundles them together into optimized packages for deployment. It can not only bundle JavaScript files, but also other project assets like [CSS files](../../css/css.md), images or fonts.

One of the main features of Webpack is its ability to manage dependencies efficiently. The dependency graph it creates allows to optimize the bundled packages by only including necessary files into the bundle. This allows for smaller bundle sizes and thus faster load times.

## Basic setup

Using Webpack requires to install the `webpack` and `webpack-cli` inside a [NPM project](npm.md).

```sh
npm i --save-dev webpack webpack-cli
```

To prevent an accidental publish of the project to the NPM registry, it is recommended to set `"private": true` and remove the `main` entry in the `package.json` file.

By default, Webpack requires a specific directory structure inside the project. All the source code should be placed inside a `./src` directory, and the output will be placed inside a `./dist` directory. The general structure should look like this:

```
my-project
|- package.json
|- package-lock.json
|- dist/   --- The bundle will be placed here
	|- index.html
	|- bundle.js
|- src/    --- The project source code will be placed here
	|- index.js
	|- my-module.js
```

This default behavior can be adjusted using a **configuration file**.

Once a project has been set up and is ready for bundling, Webpack can be executed using this command:

```sh
npx webpack
```

### Using a configuration

The recent versions of Webpack (starting at v4) don't require to use a configuration file. But as the complexity of a project grows, it is recommended to configure the default behavior of Webpack rather than having to manually execute many different commands.

Webpack will look for a `webpack.config.js` file in the project's root directory. A basic configuration could look like this:

```js
const path = require('path');

module.exports = {
	mode: 'development', // set webpack to development mode
	entry: './src/index.js', // defines the entry point
	output: {
		filename: 'bundle.js', // defines the name of the bundle file
	    path: path.resolve(__dirname, 'dist'), // defines the output directory
	    clean: true, // the output directory will be cleaned before bundling
	},
};
```

When executing Webpack, it will automatically use the `webpack.config.js` file for its configuration, if one exists. It is also possible to use a different file name for the configuration file. In this case, it has to be passed manually to Webpack by using the `--config` flag.

```sh
npx webpack --config myConfig.js
```

### Loading assets

Webpack allows to load different types of assets like CSS, images or fonts.

CSS files can be loaded by importing them into JavaScript file. This requires to install the `style-loader` and `css-loader` to be installed:

```sh
npm i --save-dev style-loader css-loader
```

They then have to be added to the configuration file:

```js
const path = require('path');

module.exports = {
	mode: 'development',
	entry: './src/index.js',
	output: {
		filename: 'bundle.js',
	    path: path.resolve(__dirname, 'dist'),
	    clean: true,
	},
	module: {
		rules: [
			{
				test: /\.css$/i,  // look for files ending with .css
				use: ['style-loader', 'css-loader'], // the loaders to use
			},	
		],
	},
};
```

Images can be loaded using the asset loaders integrated into Webpack 5:

```js
const path = require('path');

module.exports = {
	mode: 'development',
	entry: './src/index.js',
	output: {
		filename: 'bundle.js',
	    path: path.resolve(__dirname, 'dist'),
	    clean: true,
	},
	module: {
		rules: [
			{
				test: /\.css$/i,
				use: ['style-loader', 'css-loader'],
			},
			{
				test: /\.(png|svg|jpg|jpeg|gif)$/i,
				type: 'asset/resource',
			},
		],
	},
};
```

### Webpack plugins

Webpack allows to use plugins to further expand its capabilities depending on the use cases.

A very popular plugin is called `html-webpack-plugin`. It allows to define a template [HTML file](../../html/html.md). Webpack will use this template to generate the `index.html` file and automatically adds links to the bundled JavaScript file and other assets like CSS. This allows to keep the `./dist` directory clean and to store the needed HTML files somewhere else inside the project.

The plugin can be installed using the following command:

```sh
npm i --save-dev html-webpack-plugin
```

It then has to be added to the configuration file:

```js
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
	mode: 'development',
	entry: './src/index.js',
	output: {
		filename: 'bundle.js',
	    path: path.resolve(__dirname, 'dist'),
	    clean: true,
	},
	module: {
		rules: [
			{
				test: /\.css$/i,
				use: ['style-loader', 'css-loader'],
			},
			{
				test: /\.(png|svg|jpg|jpeg|gif)$/i,
				type: 'asset/resource',
			},
		],
	},
	plugins: [
		new HtmlWebpackPlugin({
			// config options
			template: "./src/index.html", // where to look for the template
			filename: "index.html", // name of the output file
		})
	]
};
```

A full list of configuration options for this plugin can be found [here](https://github.com/jantimon/html-webpack-plugin?tab=readme-ov-file#options).

### Development server

Webpack provides a simple web server that can be used for development work. It supports live reloading when a file change is detected.

To use the server, it first has to be installed:

```sh
npm i --save-dev webpack-dev-server
```

It then has to be added to the configuration file:

```js
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
	mode: 'development',
	entry: './src/index.js',
	output: {
		filename: 'bundle.js',
	    path: path.resolve(__dirname, 'dist'),
	    clean: true,
	},
	devtool: 'inline-source-map', // how to track error messages
	devServer: {
		static: './dist', // serve the contents of the ./dist directory
		// watch files ending in .html, .css and .js for changes
		watchFiles: ['./src/**/*.js', './src/**/*.html', './src/**/*.css'],
		hot: true, // enable hot reloading
	},
	module: {
		rules: [
			{
				test: /\.css$/i,
				use: ['style-loader', 'css-loader'],
			},
			{
				test: /\.(png|svg|jpg|jpeg|gif)$/i,
				type: 'asset/resource',
			},
		],
	},
	plugins: [
		new HtmlWebpackPlugin({
			template: "./src/index.html",
			filename: "index.html",
		})
	]
};
```

The server can then be started using this command:

```sh
npx webpack serve --open
```

## Splitting up the config

Webpack can be executed in either development or production mode. The goals of these two modes differ greatly:

- While in development mode, the focus should be set on options that make development easier, like strong source mapping and a local development server.
- Production mode should be used to create minified bundles and optimized assets to improve load times.

Because of this, it might make sense to use different configs during development and when making production builds. Options that stay the same in both environments are stored inside a **common configuration file**, while both development and production mode will store their options in separate files.

These specific configs will be merged with the common file. This can be achieved using the `webpack-merge` package.

```sh
npm i --save-dev webpack-merge
```

The `webpack.config.js` file will be split up into three separate files:

- `webpack.common.js`

```js
const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
    entry: "./src/index.js",
    output: {
        filename: "bundle.js",
        path: path.resolve(__dirname, "dist"),
        clean: true,
    },
    plugins: [
        new HtmlWebpackPlugin({
            template: "./src/index.html",
            filename: "index.html",
            inject: "body",
        }),
    ],
    module: {
        rules: [
            {
                test: /\.css$/i,
                use: ["style-loader", "css-loader"],
            },
            {
                test: /\.(png|svg|jpg|jpeg|gif)$/i,
                type: "asset/resource",
            },
        ],
    },
};
```

- `webpack.dev.js`

```js
const { merge } = require("webpack-merge");
const common = require("./webpack.common");

module.exports = merge(common, {
    mode: "development",
    devtool: "inline-source-map",
    devServer: {
        static: "./dist",
        watchFiles: ["./src/**/*.js", "./src/**/*.html", "./src/**/*.css"],
        hot: true,
    },
});
```

- `webpack.prod.js`

```js
const { merge } = require("webpack-merge");
const common = require("./webpack.common.js");

module.exports = merge(common, {
    mode: "production",
});
```

Using this method requires to define the used config when executing Webpack.

To start the development server:

```sh
npx webpack serve --open --config webpack.dev.js
```

To create a production build

```sh
npx webpack --config webpack.prod.js
```

## Using NPM scripts

Webpack commands can get pretty long when having to use many different flags. Because of this, it is recommended to set up some shortcuts by defining NPM scripts inside `package.json`.

```json
{
	/* ... */
	"scripts": {
		"build": "webpack --config webpack.prod.js",
		"dev": "webpack serve --open --config webpack.dev.js"
	},
	/* ... */
}
```

This allows to start the development server using `npm run dev` and to create a production build using `npm run build`.