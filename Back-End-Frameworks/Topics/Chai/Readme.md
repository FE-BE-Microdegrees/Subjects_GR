# Βιβλιοθήκη Chai Assertion 

Το Chai είναι μια δημοφιλής βιβλιοθήκη ισχυρισμών για JavaScript που χρησιμοποιείται με πλαίσια δοκιμών όπως το Mocha και το Jest. Το Chai προσφέρει διάφορα στυλ ισχυρισμών, συμπεριλαμβανομένων των στυλ TDD (Test-Driven Development) και BDD (Behavior-Driven Development), καθιστώντας εύκολη και ευανάγνωστη τη συγγραφή δοκιμών.

![Chai](Chai.webp)

Image source: Dall-E by OpenAI

- [Βιβλιοθήκη Chai Assertion](#Βιβλιοθήκη-Chai-Assertion)
  - [Μαθησιακά αποτελέσματα](#Μαθησιακά-αποτελέσματα)
  - [Τι είναι το Chai;](#Τι-είναι-το-Chai;)
    - [Πλεονεκτήματα του Chai](#Πλεονεκτήματα-του-Chai)
  - [Εγκατάσταση και ρύθμιση του Chai](#Εγκατάσταση-και-ρύθμιση-του-Chai)
    - [1. Εγκατάσταση του Chai](#1-Εγκατάσταση-του-Chai)
    - [2. Εγκατάσταση του Testing Framework](#2-Εγκατάσταση-του-Testing-Framework)
    - [3. Δημιουργία ενός αρχείου δοκιμής](#3-Δημιουργία-ενός-αρχείου-δοκιμής)
  - [Writing Tests με το Chai](#Writing-Tests-με-το-Chai)
    - [Παράδειγμα: TDD Style Test](#Παράδειγμα--:--TDD-Style-Test)
      - [`sum.js` - Η συνάρτηση που δοκιμάζουμε](#sum.js---Η-συνάρτηση-που-δοκιμάζουμε)
      - [`test/sum.test.test.js` - Δοκιμή Mocha με Chai](#test/sum.test.test.js---Δοκιμή-Mocha-με-Chai)
    - [Παράδειγμα: BDD Style Test](#Παράδειγμα--:--BDD-Style-Test)
      - [`test/sum.test.js` - Δοκιμή Mocha με Chai](#testsumtestjs---Δοκιμή-Mocha-με-Chai)
    - [Εκτέλεση Tests](#Εκτέλεση-tests)
  - [Chai Assertion Styles](#chai-assertion-styles)
    - [1. Στυλ Assert](#1-Στυλ-Assert)
    - [2. Expect Style](#2-expect-style)
    - [3. Should Style](#3-should-style)
  - [Επέκταση του Chai](#Επέκταση-του-Chai)
    - [Παράδειγμα: Chai-as-Promised](#Παράδειγμα-chai-as-promised)
      - [Εγκατάσταση](#Εγκατάσταση)
      - [Χρήση](#Χρήση)
  - [Πρόσθετα παραδείγματα και βέλτιστες πρακτικές](#Πρόσθετα-παραδείγματα-και-βέλτιστες-πρακτικές)
    - [Έλεγχος ισότητας αντικειμένων](#Έλεγχος-ισότητας-αντικειμένων)
    - [Έλεγχος για σφάλματα](#Έλεγχος-για-σφάλματα)
    - [Δοκιμή ασύγχρονων συναρτήσεων](#Δοκιμή-ασύγχρονων-συναρτήσεων)

## Μαθησιακά αποτελέσματα

Στο τέλος αυτής της ενότητας, οι εκπαιδευόμενοι θα πρέπει να είναι σε θέση να:

- εξηγήστε τι είναι το Chai και γιατί χρησιμοποιείται,
- να εγκαταστήσετε και να ρυθμίσετε το Chai σε επίπεδο έργου με το Mocha ή ένα άλλο πλαίσιο δοκιμών,
- να χρησιμοποιήσετε διάφορες δηλώσεις του Chai για τη συγγραφή δοκιμών σε στυλ TDD και BDD,
- να επεκτείνετε τη λειτουργικότητα του Chai με πρόσθετα.

## Τι είναι το Chai;

Το Chai είναι μια βιβλιοθήκη ισχυρισμών που παρέχει διάφορες μεθόδους για την επαλήθευση των αποτελεσμάτων των δοκιμών. Συνεργάζεται καλά με το Mocha και άλλα πλαίσια δοκιμών JavaScript, προσφέροντας ευέλικτους και ευανάγνωστους ισχυρισμούς.

### Πλεονεκτήματα του Chai

- **Ευελιξία:** Υποστηρίζει πολλαπλά assertion styles.
- **Αναγνωσιμότητα:** Οι ισχυρισμοί(asssertions) είναι σαφείς και διαισθητικοί.
- **Επεκτασιμότητα:** Μπορεί να επεκταθεί με plugins.

## Εγκατάσταση και ρύθμιση του Chai

### 1. Εγκατάσταση Chai

Εγκαταστήστε το Chai σε επίπεδο έργου χρησιμοποιώντας npm ή yarn.

```bash
npm install --save-dev chai@4.4.1
```

Ή, αν χρησιμοποιείτε νήματα:

```bash
yarn add --dev chai@4.4.1
```

> Σημείωση: Για αυτό το μάθημα, χρησιμοποιούμε την έκδοση 4.4.1, καθώς είναι η τελευταία έκδοση που υποστηρίζει εισαγωγές με βάση τις «απαιτήσεις». Οι νεότερες εκδόσεις χρησιμοποιούν εισαγωγές ES6.

### 2. Εγκατάσταση του  Testing Framework

Σε αυτό το παράδειγμα, θα χρησιμοποιήσουμε το Mocha, αλλά μπορείτε επίσης να χρησιμοποιήσετε το Jest ή οποιοδήποτε άλλο πλαίσιο δοκιμών.

```bash
npm install --save-dev mocha
```

Προσθέστε ένα σενάριο στο αρχείο `package.json` για την εκτέλεση δοκιμών με τη Mocha.

```json
{
  "scripts": {
    "test": "mocha"
  }
}
```

### 3. Δημιουργία ενός αρχείου δοκιμής

Δημιουργήστε έναν κατάλογο με όνομα `test` στη ρίζα του έργου και ένα αρχείο δοκιμών μέσα σε αυτόν, για παράδειγμα, `sum.test.js`.

```bash
mkdir test
cd test
touch sum.test.js
```

## Writing Tests με το Chai

### Παράδειγμα: TDD Style Test

#### `sum.js` - Η συνάρτηση που δοκιμάζουμε

```javascript
function sum(a, b) {
  return a + b;
}

module.exports = sum;
```

#### `test/sum.test.test.js` - Δοκιμή Mocha με Chai

```javascript
const chai = require("chai");
const assert = chai.assert;
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

### Παράδειγμα: TDD Style Test

#### `test/sum.test.js` - Mocha Test με το Chai

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

### Εκτέλεση Tests

Εκτελέστε τις δοκιμές χρησιμοποιώντας τη γραμμή εντολών της Mocha.

```bash
npm test
```

## Chai Assertion Styles

Chai supports three different assertion styles: Assert, Expect, and Should.

### 1. Assert Style

```javascript
const chai = require("chai");
const assert = chai.assert;

assert.strictEqual(sum(1, 2), 3, "sum of 1 and 2 should be 3");
```

### 2. Expect Style

```javascript
const chai = require("chai");
const expect = chai.expect;

expect(sum(1, 2)).to.equal(3, "sum of 1 and 2 should be 3");
```

### 3. Should Style

```javascript
const chai = require("chai");
chai.should();

sum(1, 2).should.equal(3, "sum of 1 and 2 should be 3");
```

## Extending Chai

Chai can be extended with plugins to add additional functionality.

### Example: Chai-as-Promised

Chai-as-Promised is a plugin that allows you to test promises.

#### Installation

```bash
npm install --save-dev chai-as-promised
```

#### Usage

```javascript
const chai = require("chai");
const expect = chai.expect;
const chaiAsPromised = require("chai-as-promised");

chai.use(chaiAsPromised);

function asyncFunction() {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve("Hello, World!");
    }, 1000);
  });
}

describe("Async Function", function () {
  it('should return "Hello, World!" after 1 second', function () {
    return expect(asyncFunction()).to.eventually.equal("Hello, World!");
  });
});
```

## Additional Examples and Best Practices

### Checking Object Equality

```javascript
const obj1 = { a: 1, b: 2 };
const obj2 = { a: 1, b: 2 };

expect(obj1).to.deep.equal(obj2);
```

### Checking for Errors

```javascript
function badFunction() {
  throw new Error("Something went wrong");
}

expect(badFunction).to.throw("Something went wrong");
```

### Testing Asynchronous Functions

```javascript
function asyncFunction(callback) {
  setTimeout(() => {
    callback(null, "Hello, World!");
  }, 1000);
}

describe("Async Function", function () {
  it('should return "Hello, World!" after 1 second', function (done) {
    asyncFunction(function (err, result) {
      expect(result).to.equal("Hello, World!");
      done();
    });
  });
});
```
