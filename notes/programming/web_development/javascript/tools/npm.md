# npm

The **node package manager**, commonly known as **npm**, is a command-line [package manager](../../../tools/package_manager.md) for [JavaScript](../basics/javascript.md). It grants access to a gigantic repository of code packages, tools and libraries. It allows to add such packages as **dependencies** to a project and provides an easy way to install, update and remove them as needed.

## Setting up a project

Using `npm` allows to easily set up a new project by executing the `npm init` command in the terminal after navigating to the project directory. This command will ask some questions to provide extra information about the project and create a `package.json` file in the current directory based on the answers given. To skip the questions when creating a new project, the `npm init -y` command can be used. This command will create a `package.json` containing default values.

### The 'package.json' file

The `package.json` file is a manifest file that describes the project and its dependencies. It contains metadata about the project like the name, version, dependencies and other configurations. A default `package.json` file looks like this:

```json
{
	"name": "project-name",
	"version": "1.0.0",
	"main": "index.js",
	"scripts": {
		"test": "echo \"Error: no test specified\" && exit 1"
	},
	"keywords": [],
	"author": "",
	"license": "GPL-3.0-only",
	"description": ""
}
```

The `"scripts"` section in this file can be especially useful. It allows to define custom scripts which can be executed by using the `npm run <script-name>` command. This feature is commonly used to define shortcuts for actions like building the project or starting up a development server.

## Installing dependencies

Dependencies can be installed using the `npm install <package-name>` command. There are two main types of dependencies:

- **Normal dependencies** are required at runtime so the app works, e.g. libraries used by the project.
- **Development dependencies** are only required while developing the app. These may include [linters](../../../tools/linter.md), [code formatters](../../../tools/code_formatter.md), testing utilities or tools to build the project such as [bundlers](bundling.md).

Normal dependencies are installed by using the `npm install` command together with the `--save` flag. This will add an entry under the `dependencies` section in the `package.json` file containing the package name and version information.

```sh
npm install --save <package-name>
```

Development dependencies can be installed by using the `--save-dev` flag. This will, similar to the `--save` flag, create an entry under the `devDependencies` section of the `package.json` file containing package name and version information.

```sh
npm install --save-dev <package-name>
```

When installing a package, `npm` will look for an entry in the `package.json` file and install the right package according to the information found. Installed packages will be stored in the `node_modules/` directory at the project's root directory. This directory should be ignored by [version control](../../../version_control/version_control.md), since packages can get quite large.

When cloning an existing project to a new machine, the `npm install` command can be used to automatically install all the project dependencies listed in the `package.json` file.