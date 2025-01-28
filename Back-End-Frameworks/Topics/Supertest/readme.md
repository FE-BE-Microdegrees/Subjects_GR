# Supertest: Ελέγχοντας HTTP Requests

## Εισαγωγή

Το supertest είναι μια βιβλιοθήκη JavaScript που χρησιμοποιείται για τη δοκιμή αιτημάτων HTTP σε περιβάλλον Node.js. Είναι ιδιαίτερα χρήσιμη κατά τη δοκιμή των τελικών σημείων API, καθώς σας επιτρέπει να στέλνετε εύκολα αιτήματα HTTP και να ελέγχετε τις απαντήσεις. Το supertest μπορεί να χρησιμοποιηθεί σε συνδυασμό με δημοφιλή πλαίσια δοκιμών όπως το Mocha και το Jest.

- [Supertest: Ελέγχοντας HTTP Requests](#Supertest-Ελέγχοντας-HTTP-Requests)
  - [Εισαγωγή](#Εισαγωγή)
  - [Μαθησιακά αποτελέσματα](#Μαθησιακά-αποτελέσματα)
  - [Τι είναι το Supertest;](#Τι-είναι-το-Supertest)
  - [Εγκατάσταση και ρύθμιση του Supertest](#Εγκατάσταση-και-ρύθμιση-του-Supertest)
    - [1. Εγκαθιστώντας το Supertest](#1-Εγκαθιστώντας-το-Supertest)
    - [2. Εγκατάσταση ενός Testing Framework](#2-Εγκατάσταση-ενός-Testing-Framework)
    - [3. Δημιουργία μιας απλής εφαρμογής Express](#3-Δημιουργία-μιας-απλής-εφαρμογής-Express)
      - [`app.js` - Εφαρμογή Express](#appjs---Εφαρμογή-Express)
      - [`server.js` - Ενεργοποίηση του διακομιστή](#serverjs---Ενεργοποίηση-του-διακομιστή)
  - [Συγγραφή Tests με το Supertest](#Συγγραφή-δοκιμών-με-το-Supertest)
    - [Παράδειγμα: Απλό Test](#Παράδειγμα-Απλό-Test)
      - [`__tests__/app.test.js`](#__tests__apptestjs)
    - [Παράδειγμα: Δοκιμή ενός αιτήματος POST](#Παράδειγμα-Δοκιμή-ενός-αιτήματος-POST)
      - [`__tests__/app.test.js`](#__tests__apptestjs-1)
    - [Εκτελώντας Tests](#Εκτελώντας-Tests)
  - [Πρόσθετα παραδείγματα και βέλτιστες πρακτικές](#Πρόσθετα-παραδείγματα-και-βέλτιστες-πρακτικές)
    - [1. Έλεγχος παραμέτρων](#1-Έλεγχος-παραμέτρων)
      - [`app.js` - Ενημερωμένο](#appjs---Ενημερωμένο)
      - [`__tests__/app.test.js`](#__tests__apptestjs-2)
    - [2. Έλεγχος επικεφαλίδας](#2-Έλεγχος-επικεφαλίδας)
      - [`app.js` - Ενημερωμένο](#appjs---Ενημερωμένο-1)
      - [`__tests__/app.test.js`](#__tests__apptestjs-3)
    - [3. Διαχείριση σφαλμάτων](#3-Διαχείριση-σφαλμάτων)
      - [`app.js` - Ενημερωμένο](#appjs---Ενημερωμένο-2)
      - [`__tests__/app.test.js`](#__tests__apptestjs-4)

## Μαθησιακά αποτελέσματα

Στο τέλος αυτού του υλικού, οι εκπαιδευόμενοι θα πρέπει να είναι σε θέση:

- Να εξηγούν τι είναι το Supertest και γιατί χρησιμοποιείται.
- Να εγκαθιστούν και να ρυθμίζουν το Supertest για τη συγγραφή δοκιμών.
- Να γράφουν και να εκτελούν δοκιμές που σχετίζονται με αιτήσεις HTTP χρησιμοποιώντας το Supertest.
- Να χρησιμοποιούν το Supertest με πλαίσια δοκιμών όπως το Jest.

## Τι είναι το Supertest;

Το Supertest είναι μια βιβλιοθήκη που σας επιτρέπει να κάνετε αιτήσεις HTTP σε διακομιστές Node.js και να επαληθεύετε τις απαντήσεις. Έχει σχεδιαστεί για να είναι απλή και διαισθητική, παρέχοντας αρκετές δυνατότητες που καθιστούν τον έλεγχο API εύκολο και αποτελεσματικό.

## Εγκατάσταση και ρύθμιση του Supertest

### 1. Εγκαθιστώντας το Supertest

Εγκαταστήστε το Supertest σε επίπεδο έργου χρησιμοποιώντας npm ή yarn.

```bash
npm install --save-dev supertest
```

Ή, αν χρησιμοποιείτε νήματα:

```bash
yarn add --dev supertest
```

### 2. Εγκατάσταση ενός Testing Framework

Σε αυτό το παράδειγμα, θα χρησιμοποιήσουμε το Mocha, αλλά μπορείτε επίσης να χρησιμοποιήσετε κάποιο άλλο πλαίσιο δοκιμών.

```bash
npm install --save-dev mocha
```

Προσθέστε ένα σενάριο στο αρχείο `package.json` για να εκτελείτε δοκιμές με τη Mocha.

```json
{
  "scripts": {
    "test": "mocha"
  }
}
```

### 3.  Δημιουργία μιας απλής εφαρμογής Express

Ας δημιουργήσουμε μια απλή εφαρμογή Express που θα δοκιμάσουμε με το Supertest.


#### `app.js` - Εφαρμογή Express

```javascript
const express = require("express");
const app = express();

app.get("/hello", (req, res) => {
  res.status(200).send("Hello, World!");
});

app.post("/data", (req, res) => {
  res.status(201).send({ message: "Data received" });
});

module.exports = app;
```

#### `server.js` - Ενεργοποίηση του διακομιστή

```javascript
const app = require("./app");

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});
```

## Συγγραφή Tests με το Supertest

### Παράδειγμα: Απλό Test

Ας δημιουργήσουμε μια δοκιμή για να ελέγξουμε την απόκριση της αίτησης GET στο τελικό σημείο `/hello`

#### `__tests__/app.test.js`

```javascript
const request = require("supertest");
const app = require("../app");

describe("GET /hello", () => {
  it('should return "Hello, World!"', async () => {
    const response = await request(app).get("/hello");
    expect(response.status).toBe(200);
    expect(response.text).toBe("Hello, World!");
  });
});
```

### Παράδειγμα: Δοκιμή ενός αιτήματος POST

Ας προσθέσουμε μια δοκιμή για να ελέγξουμε την απόκριση της αίτησης POST στο τελικό σημείο `/data`.

#### `__tests__/app.test.js`

```javascript
const request = require("supertest");
const app = require("../app");

describe("GET /hello", () => {
  it('should return "Hello, World!"', async () => {
    const response = await request(app).get("/hello");
    expect(response.status).toBe(200);
    expect(response.text).toBe("Hello, World!");
  });
});

describe("POST /data", () => {
  it('should return "Data received"', async () => {
    const response = await request(app).post("/data").send({ name: "John" });
    expect(response.status).toBe(201);
    expect(response.body.message).toBe("Data received");
  });
});
```

### Εκτελώντας Tests

Εκτελέστε τις δοκιμές χρησιμοποιώντας το Jest από τη γραμμή εντολών.

```bash
npm test
```

## Πρόσθετα παραδείγματα και βέλτιστες πρακτικές

### 1.  Έλεγχος παραμέτρων

Δοκιμάστε τον τρόπο με τον οποίο το API χειρίζεται τις παραμέτρους URL και τις συμβολοσειρές ερωτημάτων.

#### `app.js` - Ενημερωμένο

```javascript
app.get("/user/:id", (req, res) => {
  res.status(200).send({ id: req.params.id });
});
```

#### `__tests__/app.test.js`

```javascript
describe("GET /user/:id", () => {
  it("should return the user id", async () => {
    const userId = "12345";
    const response = await request(app).get(`/user/${userId}`);
    expect(response.status).toBe(200);
    expect(response.body.id).toBe(userId);
  });
});
```

### 2.  Έλεγχος επικεφαλίδας

Δοκιμάστε τον τρόπο με τον οποίο το API χειρίζεται τις επικεφαλίδες HTTP.

#### `app.js` - Ενημερωμένο

```javascript
app.get("/headers", (req, res) => {
  res.status(200).set("X-Custom-Header", "value").send("Headers");
});
```

#### `__tests__/app.test.js`

```javascript
describe("GET /headers", () => {
  it("should return custom header", async () => {
    const response = await request(app).get("/headers");
    expect(response.status).toBe(200);
    expect(response.headers["x-custom-header"]).toBe("value");
  });
});
```

### 3. Διαχείριση σφαλμάτων

Δοκιμάστε τον τρόπο με τον οποίο το API χειρίζεται τα σφάλματα και τις άκυρες αιτήσεις

#### `app.js` - Ενημερωμένο

```javascript
app.get("/error", (req, res) => {
  res.status(500).send({ error: "Something went wrong" });
});
```

#### `__tests__/app.test.js`

```javascript
describe("GET /error", () => {
  it("should return an error", async () => {
    const response = await request(app).get("/error");
    expect(response.status).toBe(500);
    expect(response.body.error).toBe("Something went wrong");
  });
});
```
