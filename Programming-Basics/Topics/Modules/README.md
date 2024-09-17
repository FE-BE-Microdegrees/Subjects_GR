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

## Πώς να χρησιμοποιήσετε ένα Module?

Για να χρησιμοποιήσουμε τη μονάδα, πρέπει πρώτα να την εισαγάγουμε. Αφού εισάγουμε το module, μπορούμε να το χρησιμοποιήσουμε στον κώδικά μας. Για παράδειγμα, εάν έχουμε ένα αρχείο που ονομάζεται `calculate`  που περιέχει μια συνάρτηση με το όνομα `add`, μπορούμε να εισαγάγουμε τη λειτουργική μονάδα και να χρησιμοποιήσουμε τη συνάρτηση ως εξής:

Τα περιεχόμενα του αρχείου `calculate.js` θα μπορούσαν να είναι κάπως έτσι:

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

## Παράδειγμα χρήσης Modules

Στο επόμενο παράδειγμα, δημιουργούμε ένα νέο αρχείο με το όνομα `index.js`, δημιουργούμε ένα αρχείο `calculate.js`, εξάγουμε τις συναρτήσεις `add` και `subtract` από το αρχείο `calculate.js`, εισάγουμε το `calculate.js.`  αρχείο στο αρχείο `index.js` και χρησιμοποιήστε τη συνάρτηση `προσθήκη` στον κώδικά μας.

![Using Module](UsingModule.gif)

[Click here to download the video](UsingModule.mp4)

## Ασκήσεις

Δημιουργήστε ένα αρχείο όπως περιγράφεται στις παρακάτω ασκήσεις.

Δοκιμάστε τον κώδικά σας εκτελώντας το αρχείο `index.js` χρησιμοποιώντας την εντολή `node index.js`.

### Άσκηση 1 - Βασικό Export and Require

**Στόχος**: Δημιουργήστε ένα Module και εισαγάγετε το.

**Περιγραφή**:Δημιουργήστε δύο αρχεία, `greetings.js` και `index.js`. Στο `greetings.js`, ορίστε μια συνάρτηση που εκτυπώνει `Hello, World!` στην κονσόλα. Εξαγωγή αυτής της συνάρτησης. Στο `index.js`, εισαγάγετε το `greetings.js` και καλέστε τη συνάρτηση που έχει εισαχθεί.

> Συμβουλή: Μην ξεχάσετε να χρησιμοποιήσετε τη λέξη-κλειδί `module.exports` για να εξαγάγετε τη συνάρτηση.
>
> Συμβουλή: Χρησιμοποιήστε τη λέξη-κλειδί `require` για να εισαγάγετε τη συνάρτηση.

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

### Άσκηση 2 - Εξαγωγή πολλαπλών συναρτήσεων

**Στόχος**: Εξαγωγή πολλαπλών λειτουργιών από μια μονάδα.

**Περιγραφή**: Δημιουργήστε δύο αρχεία, `greetings.js` και `index.js`. Στο `greetings.js`, ορίστε δύο συναρτήσεις, μία που εκτυπώνει "Hello, World!" στην κονσόλα και ένα που παίρνει ένα όνομα ως όρισμα και τυπώνει "Hello, [name]!" στην κονσόλα. Εξαγωγή και των δύο λειτουργιών. Στο `index.js`, εισαγάγετε το «greetings.js» και καλέστε τις εισαγόμενες συναρτήσεις.

> Συμβουλή: Μπορείτε να εξαγάγετε πολλές συναρτήσεις χρησιμοποιώντας τη λέξη-κλειδί `module.exports` ακολουθούμενη από ένα αντικείμενο που περιέχει τις συναρτήσεις που θέλετε να εξαγάγετε.

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

### Άσκηση 3 - Εξαγωγή αντικειμένου

**Στόχος**: Εξαγωγή ενός αντικειμένου που περιέχει πολλές μεθόδους.

**Περιγραφή**: Δημιουργήστε ένα αρχείο `utils.js` με ένα αντικείμενο που έχει δύο μεθόδους: `square` (επιστρέφει το τετράγωνο ενός αριθμού) και `cube` (επιστρέφει τον κύβο ενός αριθμού). Εξαγωγή αυτού του αντικειμένου. Στο `index.js`, εισαγάγετε αυτό το αντικείμενο και καλέστε τις μεθόδους του.

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


