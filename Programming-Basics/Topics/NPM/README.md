# Node Package Manager (*NPM*)

In this topic, we'll learn about Node Package Manager (NPM).

- [Node Package Manager (*NPM*)](#node-package-manager-npm)
  - [Learning Outcomes](#learning-outcomes)
  - [What is NPM?](#what-is-npm)
  - [How to Install NPM?](#how-to-install-npm)
  - [How to Use NPM?](#how-to-use-npm)
  - [How to Create a package.json File?](#how-to-create-a-packagejson-file)
  - [How to Install Packages?](#how-to-install-packages)
  - [How to Uninstall Packages?](#how-to-uninstall-packages)
  - [How to Update Packages?](#how-to-update-packages)
  - [How to Use Packages?](#how-to-use-packages)
  - [Example of Using NPM to install `ansi-colors` package and use it in code](#example-of-using-npm-to-install-ansi-colors-package-and-use-it-in-code)
    - [Commands and code used in the example](#commands-and-code-used-in-the-example)
    - [Create package.json file](#create-packagejson-file)

## Learning Outcomes

After completing this topic, you'll be able to:

- Define what NPM is
- Install NPM on your computer
- Use NPM to install, uninstall, and update packages
- Use packages in your code
- Create a `package.json` file
- Explain what `node_modules` folder is
- Explain what NPM registry is

## What is NPM?

NPM is a tool that is used to install and manage Node JS packages. It is a command-line tool that is installed along with Node JS. It is used to install packages from the [NPM registry](https://www.npmjs.com/) and to manage packages that are installed locally on our computer.

Package is a collection of files that are used to perform a specific task. For example, there are packages that are used to create web applications, packages that are used to create desktop applications, packages that are used to create mobile applications, etc.

[NPM registry](https://www.npmjs.com/) is a public repository of Node JS packages. It contains thousands of packages that can be installed using NPM.

## How to Install NPM?

NPM is installed along with Node JS. In order to install NPM, we need to download the Node JS installer from the [official Node JS website](https://nodejs.org/en/download). The installer will install Node JS and NPM on our computer.

## How to Use NPM?

In order to use NPM, we need to open a terminal and type `npm` followed by the command that we want to run. For example, if we want to install a package, we can type `npm install packageName` in the terminal, where `packageName` is the name of the package that we want to install.

## How to Create a package.json File?

package.json is a file that contains information about a Node JS project. It contains information such as the name of the project, the version of the project, the author of the project, the dependencies (packages needed for projeckt) of the project, etc. It is used by NPM to install and manage packages that are installed locally on our computer.

In order to create a `package.json` file, we need to open a terminal and type `npm init` in the terminal. This will create a `package.json` file in the current directory. We can also use `npm init -y` to create a `package.json` file with default values.

`package.json` file looks like this:

```json
{
  "name": "my-project",
  "version": "1.0.0",
  "description": "My Project",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
  },
  "author": "John Doe",
  "license": "ISC",
  "dependencies": {
    "packageName": "1.0.0"
  }
}
```

## How to Install Packages?

In order to install a package, we need to open a terminal and type `npm install packageName` in the terminal, where `packageName` is the name of the package that we want to install. This will install the package in the `node_modules` folder in the current directory and add it to the `dependencies` section of the `package.json` file.

`node_modules` folder contains all the packages that are installed locally on our computer. It is created automatically when we install a package using NPM.

```bash	
npm install packageName
```

Installing package using NPM will also create a `package-lock.json` file in the current directory. This file contains information about the exact version of each package that is installed in the `node_modules` folder. It is used by NPM to install the exact same version of each package when we run `npm install` command.

## How to Uninstall Packages?

In order to uninstall a package, we need to open a terminal and type `npm uninstall packageName` in the terminal, where `packageName` is the name of the package that we want to uninstall. This will uninstall the package from the `node_modules` folder in the current directory and remove it from the `dependencies` section of the `package.json` file.

```bash
npm uninstall packageName
```

## How to Update Packages?

In order to update a package, we need to open a terminal and type `npm update packageName` in the terminal, where `packageName` is the name of the package that we want to update. This will update the package in the `node_modules` folder in the current directory and update it in the `dependencies` section of the `package.json` file.

```bash
npm update packageName
```

## How to Use Packages?

In order to use a package, we need to import it in our code using the `require()` function. For example, if we want to use the `packageName` package, we can import it using the following code:

```javascript
const packageName = require('packageName');
```

## Example of Using NPM to install `ansi-colors` package and use it in code

[`ansi-colors`](https://www.npmjs.com/package/ansi-colors) package is a package that is used to add colors to the text in the terminal.

In next example, we create a new file named `index.js`, create a `package.json` file using `npm init -y` command, install the `ansi-colors` package using `npm install ansi-colors` command, and use the `ansi-colors` package in our code.

![Using NPM](UsingNPM.gif)

### Commands and code used in the example

```bash
npm init -y
npm install ansi-colors
```

```javascript
const colors = require('ansi-colors');

console.log(colors.red('Hello world!'));
console.log(colors.yellow('Hello world!'));
console.log(colors.green('Hello world!'));
```

```bash
node index.js
```

### Create package.json file

```json
{
  "name": "nodejs",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "ansi-colors": "^4.1.3"
  }
}
```

