# Modules

In this topic, we'll learn about modules in Javascript.

- [Modules](#modules)
  - [Learning Outcomes](#learning-outcomes)
  - [What is a Module?](#what-is-a-module)
  - [How to Export a Module?](#how-to-export-a-module)
  - [How to Import a Module?](#how-to-import-a-module)
  - [How to Use a Module?](#how-to-use-a-module)
  - [Example of Using Modules](#example-of-using-modules)
  - [Exercises](#exercises)
    - [Exercise 1 - Basic Export and Require](#exercise-1---basic-export-and-require)
    - [Exercise 2 - Export Multiple Functions](#exercise-2---export-multiple-functions)
    - [Exercise 3 - Exporting an Object](#exercise-3---exporting-an-object)

## Learning Outcomes

After completing this topic, you'll be able to:

- Define what a module is
- Explain how to export a module
- Explain how to import a module
- Explain how to use a module

## What is a Module?

A module is a Javascript file that contains code that can be reused in other Javascript files. Modules are used to organize code into logical units that can be reused in other parts of the program. Modules are used to create reusable code that can be used in other programs.

## How to Export a Module?

In order to export a module, we need to use the `module.exports` keyword followed by the name of the module that we want to export. For example, if we want to export a module named `myModule`, we can type `module.exports myModule;` or `module.exports { myModule, myModule1 };` (if we have multiple exports) in the Javascript file where we want to export the module.

```javascript
module.exports myModule; // export a module named myModule
```
or
```javascript
module.exports { myModule, myModule1 }; // export multiple modules named myModule and myModule1
```

## How to Import a Module?

In order to import a module, we need to use the `require` keyword followed by the name of the file containing module(s) that we want to import. For example, if we want to import a module named `myModule` from file `moduleFileName.js`, we can type `require('./moduleFileName');` in the Javascript file where we want to import the module (the `./` part is used to specify the path to the file containing the module(s) that we want to import). 

```javascript
const myModule = require('./moduleFileName'); // import a module from file named `moduleFileName.js`
```
or
```javascript
import { myModule, myModule1 } from './moduleFileName'; // import multiple modules named myModule and myModule1 from the `moduleFileName.js` file
```

## How to Use a Module?

To use module, we need to import it first. After we import the module, we can use it in our code. For example, if we have file called `calculate` that contains a function named `add`, we can import the module and use the function like this:

Contents of `calculate.js` file could be something like this:

```javascript
function add(a, b) {
  return a + b;
}

function subtract(a, b) {
  return a - b;
}

module.exports = { add, subtract }; // export the add and subtract functions
```

Contents of `index.js` file could be something like this:

```javascript
const calculate = require('./calculate'); // import the calculate module

const sum = calculate.add(5, 3); // call the add function from the calculate module and assign the result to the sum variable

console.log(sum); // print the value of the sum variable to the console
```

## Example of Using Modules

In next example, we create a new file named `index.js`, create a `calculate.js` file, export the `add` and `subtract` functions from the `calculate.js` file, import the `calculate.js` file in the `index.js` file, and use the `add` function in our code.

![Using Module](UsingModule.gif)

[Click here to download the video](UsingModule.mp4)

## Exercises

Create a files as described in the exercises below.

Test your code by running the `index.js` file using the `node index.js` command.

### Exercise 1 - Basic Export and Require

**Objective**: Create a basic module and import it.

**Description**: Create two files, `greetings.js` and `index.js`. In `greetings.js`, define a function that prints "Hello, World!" to the console. Export this function. In `index.js`, import `greetings.js` and call the imported function.

> Hint: Don't forget to use the `module.exports` keyword to export the function.
>
> Hint: Use the `require` keyword to import the function.

<details>
  <summary>Solution</summary>

  ```javascript
  // greetings.js
  function sayHello() {
    console.log('Hello, World!');
  }

  module.exports = sayHello;
  ```

  ```javascript
  // index.js
  const sayHello = require('./greetings');

  sayHello();
  ```
![Modules](modules.gif)
</details>

### Exercise 2 - Export Multiple Functions

**Objective**: Export multiple functions from a module.

**Description**: Create two files, `greetings.js` and `index.js`. In `greetings.js`, define two functions, one that prints "Hello, World!" to the console and one that takes a name as an argument and prints "Hello, [name]!" to the console. Export both functions. In `index.js`, import `greetings.js` and call the imported functions.

> Hint: You can export multiple functions by using the `module.exports` keyword followed by an object containing the functions that you want to export.

<details>
  <summary>Solution</summary>

  ```javascript
  // greetings.js
  function sayHello() {
    console.log('Hello, World!');
  }

  function sayHelloTo(name) {
    console.log(`Hello, ${name}!`);
  }

  module.exports = { sayHello, sayHelloTo };
  ```

  ```javascript
  // index.js
  const { sayHello, sayHelloTo } = require('./greetings');

  sayHello();
  sayHelloTo('John');
  ```
</details>

### Exercise 3 - Exporting an Object

**Objective**: Export an object containing multiple methods.

**Description**: Create a file `utils.js` with an object that has two methods: `square` (returns the square of a number) and `cube` (returns the cube of a number). Export this object. In `index.js`, import this object and call its methods.

> Hint: You can add functions to an object using the following syntax:
> ```javascript
> const myObject = {
>   myFunction() {
>     // function body
>   }
> }
> ```
>
> Hint: You can call a function from an object using the following syntax:
> ```javascript
> myObject.myFunction();
> ```


