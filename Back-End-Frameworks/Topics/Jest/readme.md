# Πλαίσιο δοκιμών Jest

## Εισαγωγή

Το Jest είναι ένα δημοφιλές και ισχυρό πλαίσιο δοκιμών που χρησιμοποιείται κυρίως για τον έλεγχο έργων JavaScript και React. Παρέχει πλούσια λειτουργικότητα για τη συγγραφή και εκτέλεση δοκιμών μονάδας, ολοκλήρωσης και end-to-end. Σχεδιασμένο για να είναι απλό και φιλικό προς το χρήστη, το Jest περιλαμβάνει ενσωματωμένες λειτουργίες όπως το mocking και τα περιβάλλοντα δοκιμών.

---

## Μαθησιακά αποτελέσματα

Στο τέλος αυτού του σεμιναρίου, οι εκπαιδευόμενοι θα πρέπει να είναι σε θέση να:

- Να εξηγούν τι είναι το Jest και γιατί χρησιμοποιείται.
- Να εγκαθιστούν και να ρυθμίζουν το Jest για δοκιμές.
- Να γράφουν και να εκτελούν βασικές δοκιμές χρησιμοποιώντας το Jest.
- Να χρησιμοποιούν τα ενσωματωμένα χαρακτηριστικά του Jest, όπως το mocking και τα περιβάλλοντα δοκιμών.

---

## Τι είναι το Jest;

Το Jest είναι ένα πλαίσιο δοκιμών JavaScript που δημιουργήθηκε από το Facebook. Είναι ιδανικό για τη δοκιμή εφαρμογών React, αλλά είναι αρκετά ευέλικτο ώστε να μπορεί να χρησιμοποιηθεί και για άλλα έργα JavaScript. Το Jest προσφέρει ενσωματωμένες λειτουργικότητες, όπως mocking, προσωρινά περιβάλλοντα και επεκτασιμότητα.

### Πλεονεκτήματα του Jest

- **Λύση All-in-One:** Το Jest περιλαμβάνει όλα όσα απαιτούνται για δοκιμές χωρίς να απαιτούνται πρόσθετα εργαλεία.
- **Εύκολη εγκατάσταση:** Το Jest είναι απλό στην εγκατάσταση και τη χρήση.
- **Απόδοση:** Το Jest μπορεί να εκτελεί δοκιμές παράλληλα, καθιστώντας τις δοκιμές γρήγορες και αποτελεσματικές.
- **Ενσωματωμένο Mocking:** Η Jest περιλαμβάνει εγγενή υποστήριξη για mocking, απλοποιώντας τη σύνταξη πολύπλοκων δοκιμών.

---

## Εγκατάσταση και ρύθμιση του Jest

### 1. Εγκατάσταση του Jest

Εγκαταστήστε το Jest ως εξάρτηση dev στο έργο σας:

```bash
npm install --save-dev jest
```

Ή, αν χρησιμοποιείτε νήματα:

```bash
yarn add --dev jest
```

### 2. Προσθήκη σεναρίου στο `package.json` 

Προσθέστε ένα σενάριο για την εκτέλεση δοκιμών Jest:

```json
{
  "scripts": {
    "test": "jest"
  }
}
```

### 3. Δημιουργήστε ένα Test File

Δημιουργήστε έναν κατάλογο με όνομα `__tests__` στη ρίζα του έργου σας και προσθέστε ένα αρχείο δοκιμών, π.χ. `sum.test.js`.

```bash
mkdir __tests__
cd __tests__
touch sum.test.js
```

## Συγγραφή δοκιμών με Jest

### Παράδειγμα: Βασική δοκιμή

#### `sum.js` - Λειτουργία προς δοκιμή

```javascript
function sum(a, b) {
  return a + b;
}

module.exports = sum;
```

#### `__tests__/sum.test.js` - Jest Test

```javascript
const sum = require('../sum');

test('adds 1 + 2 to equal 3', () => {
  expect(sum(1, 2)).toBe(3);
});

test('adds -2 + 1 to equal -1', () => {
  expect(sum(-2, 1)).toBe(-1);
});
```

### Εκτέλεση δοκιμών

Εκτελέστε δοκιμές χρησιμοποιώντας την εντολή Jest:

```bash
npm test
```

## Δοκιμή ασύγχρονου κώδικα

Η Jest υποστηρίζει ασύγχρονες δοκιμές χρησιμοποιώντας callbacks, υποσχέσεις, o `async`/`await` 

### Παράδειγμα: Δοκιμή υποσχέσεων

#### `asyncFunction.js` - Ασύγχρονη λειτουργία

```javascript
function asyncFunction() {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve('Hello World');
    }, 1000);
  });
}

module.exports = asyncFunction;
```

#### `__tests__/asyncFunction.test.js` - Jest test

```javascript
const asyncFunction = require('../asyncFunction');

test('async function returns "Hello World" after 1 second', () => {
  return asyncFunction().then(data => {
    expect(data).toBe('Hello World');
  });
});
```

### Παράδειγμα: Χρήση `async`/`await`

#### `__tests__/asyncFunctionAsync.test.js` - Jest test

```javascript
const asyncFunction = require('../asyncFunction');

test('async function returns "Hello World" after 1 second', async () => {
  const data = await asyncFunction();
  expect(data).toBe('Hello World');
});
```

## Mocking with Jest

Jest provides built-in support for mocking modules and functions to test code in isolation.

### Example: Mocking a Function

#### `fetchData.js` - Λειτουργία προς δοκιμή

```javascript
const axios = require('axios');

async function fetchData() {
  const response = await axios.get('https://api.example.com/data');
  return response.data;
}

module.exports = fetchData;
```

#### `__tests__/fetchData.test.js` - Jest Test με Mocking

```javascript
const fetchData = require('../fetchData');
const axios = require('axios');

jest.mock('axios');

test('fetches data from API', async () => {
  const data = { name: 'John Doe' };
  axios.get.mockResolvedValue({ data });

  const result = await fetchData();
  expect(result).toEqual(data);
});
```

## Test Environment με Hooks

Η Jest παρέχει άγκιστρα όπως (`beforeEach`, `afterEach`, `beforeAll`, `afterAll`) για την εκτέλεση κώδικα πριν και μετά τις δοκιμές.

### Παράδειγμα: Χρήση αγκίστρων

```javascript
let data;

beforeAll(() => {
  data = { name: 'John Doe' };
});

afterAll(() => {
  data = null;
});

test('data name is John Doe', () => {
  expect(data.name).toBe('John Doe');
});
```
