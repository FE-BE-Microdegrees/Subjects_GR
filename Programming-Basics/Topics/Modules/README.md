# Module

Σε αυτή τη θεματική ενότητα, θα μάθουμε για τις ενότητες σε Javascript.

- [Module](#Module)
  - [Μαθησιακά Αποτελέσματα](#Μαθησιακά-Αποτελέσματα)
  - [Τι είναι ένα Module;](#Τι-είναι-ένα-Module-;)
  - [Πώς να εξαγάγετε ένα Module?](#Πώς-να-εξαγάγετε-ένα-Module-?)
  - [Πώς να εισαγάγετε ένα Module?](#Πώς-να-εισαγάγετε-ένα-Module-?)
  - [Πώς να χρησιμοποιήσετε ένα Module?](#Πώς-να-χρησιμοποιήσετε-ένα-Module-?)
  - [Παράδειγμα χρήσης Modules](#Παράδειγμα-χρήσης-Modules)
  - [Άσκησεις](#Άσκησεις)
    - [Άσκηση 1 - Βασικό Export and Require](#Άσκηση-1---Βασικό-Export-and-Require)
    - [Άσκηση 2 - Εξαγωγή πολλαπλών συναρτήσεων](#Άσκηση-2---Εξαγωγή-πολλαπλών-συναρτήσεων)
    - [Άσκηση 3 - Εξαγωγή αντικειμένου](#Άσκηση-3---Εξαγωγή-αντικειμένου)

## Μαθησιακά Αποτελέσματα

Αφού ολοκληρώσετε αυτή τη θεματική ενότητα , θα είστε σε θέση:

- Ορίστε τι είναι ένα module
- Εξηγήστε πώς να εξαγάγετε ένα module
- Εξηγήστε τον τρόπο εισαγωγής ενός module
- Εξηγήστε πώς να χρησιμοποιήσετε ένα module
- 
## Τι είναι ένα Module;

Μια λειτουργική μονάδα είναι ένα αρχείο Javascript που περιέχει κώδικα που μπορεί να επαναχρησιμοποιηθεί σε άλλα αρχεία Javascript. Οι μονάδες χρησιμοποιούνται για την οργάνωση κώδικα σε λογικές μονάδες που μπορούν να επαναχρησιμοποιηθούν σε άλλα μέρη του προγράμματος. Οι μονάδες χρησιμοποιούνται για τη δημιουργία επαναχρησιμοποιήσιμου κώδικα που μπορεί να χρησιμοποιηθεί σε άλλα προγράμματα.

## Πώς να εισαγάγετε ένα Module?

Για να εξαγάγουμε μια λειτουργική μονάδα, πρέπει να χρησιμοποιήσουμε τη λέξη-κλειδί `module.exports` ακολουθούμενη από το όνομα της λειτουργικής μονάδας που θέλουμε να εξαγάγουμε. Για παράδειγμα, εάν θέλουμε να εξαγάγουμε μια λειτουργική μονάδα με το όνομα `myModule`, μπορούμε να πληκτρολογήσουμε `module.exports myModule;` ή `module.exports { myModule, myModule1 };` (αν έχουμε πολλές εξαγωγές) στο αρχείο Javascript όπου πληκτρολογούμε θέλετε να εξαγάγετε τη μονάδα.

```javascript
module.exports myModule; // export a module named myModule
```
or
```javascript
module.exports { myModule, myModule1 }; // export multiple modules named myModule and myModule1
```

## Πώς να εισαγάγετε ένα Module?

Για να εισαγάγουμε μια λειτουργική μονάδα, πρέπει να χρησιμοποιήσουμε τη λέξη-κλειδί `require` ακολουθούμενη από το όνομα του αρχείου που περιέχει τις λειτουργικές μονάδες που θέλουμε να εισαγάγουμε. Για παράδειγμα, εάν θέλουμε να εισαγάγουμε μια λειτουργική μονάδα με το όνομα `myModule` από το αρχείο `moduleFileName.js`, μπορούμε να πληκτρολογήσουμε `require('./moduleFileName»);` στο αρχείο Javascript όπου θέλουμε να εισαγάγουμε τη λειτουργική μονάδα (το  τμήμα `./` χρησιμοποιείται για να καθορίσει τη διαδρομή προς το αρχείο που περιέχει τις λειτουργικές μονάδες που θέλουμε να εισαγάγουμε.

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


