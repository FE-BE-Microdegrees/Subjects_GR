# Mocha Testing Framework

Το Mocha είναι ένα δημοφιλές πλαίσιο δοκιμών JavaScript που σας επιτρέπει να γράφετε και να εκτελείτε δοκιμές τόσο σε περιβάλλοντα από την πλευρά του διακομιστή (Node.js) όσο και από την πλευρά του πελάτη (πρόγραμμα περιήγησης). Το Mocha είναι ευέλικτο και επεκτάσιμο, υποστηρίζοντας διάφορα στυλ δοκιμών, συμπεριλαμβανομένων των BDD (Behavior-Driven Development) και TDD (Test-Driven Development).


- [Mocha Testing Framework](#mocha-testing-framework)
  - [Μαθησιακά αποτελέσματα](#Μαθησιακά-αποτελέσματα)
  - [Τι είναι το Mocha;](#Τι-είναι-το-Mocha)
  - [Πλεονεκτήματα του Mocha](#Πλεονεκτήματα-της-Mocha)
  - [Εγκατάσταση και ρύθμιση του Mocha](#Εγκατάσταση-και-ρύθμιση-της-Mocha)
    - [1. Εγκαθιστώντας το Mocha](#1-Εγκαθιστώντας-το-Mocha)
      - [Καθολική εγκατάσταση](#Καθολική-εγκατάσταση)
      - [Project-Level Εγκατάσταση](#project-level-Εγκατάσταση)
    - [2. Δημιουργία ενός Test File](#2-Δημιουργία-ενός-test-file)
  - [Συγγραφή δοκιμών με τη Mocha](#Συγγραφή-δοκιμών-με-τη-Mocha)
    - [Παράδειγμα: Simple Test](#Παράδειγμα-simple-test)
      - [`sum.js` - Συνάρτηση για Test](#sumjs---Συνάρτηση-για-Test)
      - [`test/test.js` - Mocha Test](#testtestjs---mocha-test)
    - [Εκτέλεση Tests](#Εκτέλεση-tests)
  - [Ασύγχρονα Tests](#Ασύγχρονα-tests)
    - [Παράδειγμα: Ασύγχρονα Test με Callbacks](#Παράδειγμα-Ασύγχρονα-Test-με-Callbacks)
      - [`asyncFunction.js` - Ασύγχρονη Function](#asyncfunctionjs---Ασύγχρονη-function)
      - [`test/asyncTest.js` - Mocha Test](#testasynctestjs---mocha-test)
    - [Παράδειγμα: Ασύγχρονο Test με Promises](#Παράδειγμα-Ασύγχρονο-Test-με-Promises)
      - [`asyncPromise.js` - Ασύγχρονη Function](#asyncpromisejs---Ασύγχρονη-function)
      - [`test/asyncPromiseTest.js` - Mocha Test](#testasyncpromisetestjs---mocha-test)
  - [Χρησιμοποιώντας Chai Assertion Library](#Χρησιμοποιώντας-chai-assertion-library)
    - [Εγκαθιστώντας το Chai](#Εγκαθιστώντας-το-Chai)
    - [Παράδειγμα: Χρησιμοποιώντας Chai](#Παράδειγμα-Χρησιμοποιώντας-Chai)
      - [`test/chaiTest.js` - Δοκιμή Mocha με Chai](#testchaitestjs---Δοκιμή-Mocha-με-Chai)
  - [Πρόσθετα χαρακτηριστικά της Mocha](#Πρόσθετα-χαρακτηριστικά-της-Mocha)
    - [Hooks](#hooks)
      - [Παράδειγμα: Χρήση Hooks](#Παράδειγμα-Χρήση-hooks)

## Μαθησιακά αποτελέσματα

Στο τέλος αυτού του υλικού, οι εκπαιδευόμενοι θα πρέπει να είναι σε θέση να:

- να εξηγούν τι είναι η Mocha και γιατί χρησιμοποιείται,
- να εγκαθιστούν και να ρυθμίζουν το πλαίσιο δοκιμών Mocha,
- να γράφουν και να εκτελούν βασικές δοκιμές χρησιμοποιώντας το Mocha,
- να χρησιμοποιούν βιβλιοθήκες ισχυρισμών όπως το Chai παράλληλα με το Mocha.

## Τι είναι το Mocha;

Το Mocha είναι ένα πλαίσιο δοκιμών JavaScript που έχει σχεδιαστεί για τη συγγραφή και εκτέλεση ασύγχρονων δοκιμών. Παρέχει έναν απλό και ευέλικτο τρόπο οργάνωσης και διαχείρισης δοκιμών και ενσωματώνεται καλά με άλλα εργαλεία και πλαίσια.

## Πλεονεκτήματα του Mocha

- **Ευελιξία:** Υποστηρίζει διάφορα στυλ και μεθοδολογίες δοκιμών.
- **Ασυγχρονικότητα:** Εύκολη συγγραφή και εκτέλεση ασύγχρονων δοκιμών.
- **Επεκτασιμότητα:** Ενσωματώνεται καλά με άλλα εργαλεία και πλαίσια, όπως το Chai και το Sinon.
- **Καλή τεκμηρίωση και κοινότητα:** Μεγάλη βάση χρηστών και άφθονοι πόροι.

## Εγκατάσταση και ρύθμιση του Mocha

### 1. Εγκαθιστώντας το Mocha

Μπορείτε να εγκαταστήσετε τη Mocha είτε συνολικά είτε σε επίπεδο έργου χρησιμοποιώντας το npm.

#### Καθολική εγκατάσταση

```bash
npm install --global mocha
```

#### Project-Level Εγκατάσταση

```bash
npm install --save-dev mocha
```

### 2. Creating a Test File

Create a directory named `test` in the root of your project and create a test file inside it, for example, `test.js`.

```bash
mkdir test
cd test
touch test.js
```

## Writing Tests with Mocha

Mocha uses BDD style functions to write tests, including `describe`, `it`, and `before`, `after`, `beforeEach`, `afterEach`.

### Example: Simple Test

#### `sum.js` - Function to Test

```javascript
function sum(a, b) {
  return a + b;
}

module.exports = sum;
```

#### `test/test.js` - Mocha Test

```javascript
const assert = require("assert");
const sum = require("../sum");

describe("Sum Function", function () {
  it("should return 3 when the inputs are 1 and 2", function () {
    assert.strictEqual(sum(1, 2), 3);
  });

  it("should return -1 when the inputs are -2 and 1", function () {
    assert.strictEqual(sum(-2, 1), -1);
  });
});
```

### Running Tests

Run the tests using Mocha from the command line.

```bash
npx mocha
```

## Asynchronous Tests

Mocha supports writing asynchronous tests using callbacks or promises.

### Example: Asynchronous Test with Callbacks

#### `asyncFunction.js` - Asynchronous Function

```javascript
function asyncFunction(callback) {
  setTimeout(() => {
    callback(null, "Hello World");
  }, 1000);
}

module.exports = asyncFunction;
```

#### `test/asyncTest.js` - Mocha Test

```javascript
const assert = require("assert");
const asyncFunction = require("../asyncFunction");

describe("AsyncFunction", function () {
  it('should return "Hello World" after 1 second', function (done) {
    asyncFunction(function (err, result) {
      assert.strictEqual(result, "Hello World");
      done();
    });
  });
});
```

### Example: Asynchronous Test with Promises

#### `asyncPromise.js` - Asynchronous Function

```javascript
function asyncPromise() {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve("Hello World");
    }, 1000);
  });
}

module.exports = asyncPromise;
```

#### `test/asyncPromiseTest.js` - Mocha Test

```javascript
const assert = require("assert");
const asyncPromise = require("../asyncPromise");

describe("AsyncPromise", function () {
  it('should return "Hello World" after 1 second', function () {
    return asyncPromise().then((result) => {
      assert.strictEqual(result, "Hello World");
    });
  });
});
```

## Using Chai Assertion Library

Chai is a popular assertion library that can be used with Mocha. Chai supports various assertion styles, including TDD and BDD.

### Installing Chai

Install Chai at the project level.

```bash
npm install --save-dev chai
```

### Example: Using Chai

#### `test/chaiTest.js` - Mocha Test with Chai

```javascript
const chai = require("chai");
const expect = chai.expect;
const sum = require("../sum");

describe("Sum Function", function () {
  it("should return 3 when the inputs are 1 and 2", function () {
    expect(sum(1, 2)).to.equal(3);
  });

  it("should return -1 when the inputs are -2 and 1", function () {
    expect(sum(-2, 1)).to.equal(-1);
  });
});
```

## Additional Mocha Features

### Hooks

Mocha provides hooks (`before`, `after`, `beforeEach`, `afterEach`) that allow you to execute code before and after tests run.

#### Example: Using Hooks

```javascript
describe("Hooks Example", function () {
  before(function () {
    // Executed before all tests
  });

  after(function () {
    // Executed after all tests
  });

  beforeEach(function () {
    // Executed before each test
  });

  afterEach(function () {
    // Executed after each test
  });

  it("test case 1", function () {
    // Test code
  });

  it("test case 2", function () {
    // Test code
  });
});
```
