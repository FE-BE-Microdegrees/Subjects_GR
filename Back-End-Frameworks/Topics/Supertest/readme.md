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

## Learning Outcomes

By the end of this material, learners should be able to:

- Explain what Supertest is and why it is used.
- Install and set up Supertest for writing tests.
- Write and run tests related to HTTP requests using Supertest.
- Use Supertest with testing frameworks like Jest.

## What is Supertest?

Supertest is a library that allows you to make HTTP requests to Node.js servers and verify responses. It is designed to be simple and intuitive, providing several features that make API testing easy and effective.

## Installing and Setting Up Supertest

### 1. Installing Supertest

Install Supertest at the project level using npm or yarn.

```bash
npm install --save-dev supertest
```

Or, if you are using yarn:

```bash
yarn add --dev supertest
```

### 2. Installing a Testing Framework

In this example, we will use Mocha, but you can also use another testing framework.

```bash
npm install --save-dev mocha
```

Add a script to your `package.json` file to run tests with Mocha.

```json
{
  "scripts": {
    "test": "mocha"
  }
}
```

### 3. Creating a Simple Express Application

Let's create a simple Express application that we will test with Supertest.

#### `app.js` - Express Application

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

#### `server.js` - Starting the Server

```javascript
const app = require("./app");

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});
```

## Writing Tests with Supertest

### Example: Simple Test

Let's create a test to check the response of the GET request to the `/hello` endpoint.

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

### Example: Testing a POST Request

Let's add a test to check the response of the POST request to the `/data` endpoint.

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

### Running Tests

Run the tests using Jest from the command line.

```bash
npm test
```

## Additional Examples and Best Practices

### 1. Parameter Checking

Test how the API handles URL parameters and query strings.

#### `app.js` - Updated

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

### 2. Header Checking

Test how the API handles HTTP headers.

#### `app.js` - Updated

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

### 3. Error Handling

Test how the API handles errors and invalid requests.

#### `app.js` - Updated

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
