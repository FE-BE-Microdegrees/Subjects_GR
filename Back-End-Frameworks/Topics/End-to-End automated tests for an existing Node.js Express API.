# Kuidas olemasolevale Node Express API-le testid lisada?

In this section, we will explore how to create End-to-End automated tests for an existing Node.js Express API.

We will use the [Mocha](../mocha/README.md) testing framework, the [Supertest](../supertest/README.md) module, and [Chai](../chai/README.md) assertions.

## Learning Outcomes

By the end of this section, students should be able to:

- Create tests for an existing Node.js Express API.
- Use the Mocha testing framework.
- Use the Supertest module.
- Use Chai assertions.
- Generate coverage reports for tests.
- Utilize a test database when writing tests.
- Separate application logic from server startup.
- Structure an application for writing tests.

## Application Structure

The first step to adding automated tests to your existing Node.js Express API is to separate the Express `app` from its initialization. This is necessary so that we can use the `app` variable during testing without directly starting the server.

To do this, we will extract the `app` creation logic from the existing `index.ts` file and leave only the server startup. This means our `index.ts` file should look like this:

```typescript
import app from "./app";

const port = process.env.PORT || 3000;

app.listen(port, () => {
  console.log(`Server running on port ${port}`);
});
```

Next, we will create a new file `app.ts`, where we will place all the code related to creating the `app`. This means our `app.ts` file should look like this:

```typescript
import express from "express";

const app = express();

app.use(express.json());

app.get("/", (_req, res) => {
  res.send("Hello World!");
});

export default app;
```

With this structure, we can import the application (`app`) into our tests and use it without starting the server.

## Test Data Creation and Test Database Usage

Next, we need to determine how to obtain the data required for testing our application. Since our goal is to test the application as it would be used in production, we want to ensure it interacts correctly with the database.

To get the necessary data for testing, we have several options:

- Use the existing live database.
- Create a new database.
- Use an in-memory database instead of a real database.
- Use a mock database instead of a real database.

Using the existing live database has significant drawbacks, such as polluting it with test data and not being able to guarantee that the data is in the expected state.

To avoid these issues, we need to create a new database for testing.

### Automating Database Creation

To automate the creation of a new database, we will write a separate script that creates the database and inserts the necessary data.

```ts
import mysql2 from "mysql2";
import path from "path";
import fs from "fs";
import config from "./config";

const dbConfig = config.db.test;

const sqlFilePath = path.join(__dirname, "init.sql");
const sqlContent = fs.readFileSync(sqlFilePath, "utf-8").toString();
const db = mysql2.createConnection(dbConfig).promise();

const statements = sqlContent.split(/;\s*$/m);

async function runQuery(sql: string) {
  try {
    await db.query(sql);
  } catch (error) {
    console.log("Error", error);
  }
}

try {
  await db.beginTransaction();
  for (const statement of statements) {
    if (statement.trim().length > 0) {
      await runQuery(statement);
    }
  }
  await db.commit();
} catch (error) {
  console.log(error);
  await db.rollback();
} finally {
  await db.end();
}
```

This script requires an `init.sql` file containing the necessary SQL commands to set up the database. For example, the `init.sql` file might look like this:

```sql
DROP DATABASE IF EXISTS `test`;

CREATE DATABASE IF NOT EXISTS `test`;

USE `test`;

CREATE TABLE IF NOT EXISTS `users` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(255) NOT NULL,
  `email` varchar(255) NOT NULL,
  `password` varchar(255) NOT NULL,
  PRIMARY KEY (`id`)
);

INSERT INTO `users` (`name`, `email`, `password`) VALUES
('John Doe', 'john@doe.ee', 'secret');
```

Now we can run this script before running our tests by adding a new script in the `package.json`:

```json
{
  "scripts": {
    "pretest": "ts-node ./scripts/create-test-db.js"
  }
}
```

The `pretest` script ensures that the database setup script runs before the tests.

Next, we need to ensure that when we run our tests, the test database is used. One way to achieve this is by using an environment variable to inform the application which database to use. To do this, we'll modify the database configuration file to select the appropriate database based on the environment variable.

Our `config.ts` file might look like this:

```ts
const config: IConfig = {
  port: 3000,
  jwtSecret: "veryStrongSecret",
  jwtExpiresIn: "1h",
  saltRounds: 10,
  db: {
    development: {
      host: "localhost",
      user: "root",
      password: "justStrongSecret",
      database: "homeworks",
    },
    test: {
      host: "localhost",
      user: "root",
      password: "justStrongSecret",
      database: "test",
    },
  },
};

export default config;
```

Next, we need to add functionality to read the environment variable and return the appropriate database configuration. This could look like:

```ts
import mysql2 from "mysql2";
import config from "./config";

const dbConfig = config.db[process.env.NODE_ENV || "development"];

const db = mysql2.createConnection(dbConfig).promise();

export default db;
```

If TypeScript gives an error about `process.env.NODE_ENV`, we can define an interface for configuration that allows any string key but requires the value to be a database configuration object.

### Example Configuration Interface

```ts
interface IDatabaseConfig {
  [key: string]: {
    host: string;
    user: string;
    password: string;
    database: string;
  };
}
```

It’s also advisable to define an interface for the entire `config.ts` file:

```ts
interface Config {
  port: number;
  jwtSecret: string;
  jwtExpiresIn: string;
  saltRounds: number;
  db: {
    [key: string]: {
      host: string;
      user: string;
      password: string;
      database: string;
    };
  };
}
```

Next, we need to ensure that tests are executed in the correct environment. One way to do this is by using the `cross-env` module. First, we install `cross-env`:

```bash
npm install cross-env
```

Then we can add the environment variable to our `package.json`:

```json
{
  "scripts": {
    "pretest": "ts-node ./scripts/create-test-db.js",
    "test": "cross-env NODE_ENV=test mocha -r ts-node/register 'tests/*.test.ts' --exit"
  }
}
```

Now, when we run `npm test`, the script to create the test database will execute before running the tests.

## Installing Testing Frameworks

Next, we need to install the necessary frameworks and type definitions for writing tests. We will install [Mocha](../mocha/README.md), [Supertest](../supertest/README.md), and [Chai](../chai/README.md):

```bash
npm install mocha supertest chai
npm install -D @types/mocha @types/supertest @types/chai
```

Additionally, we need to update the ESLint configuration to avoid warnings about Chai assertions. First, we need to install the `eslint-plugin-chai-friendly` module:

```bash
npm install eslint-plugin-chai-friendly --save-dev
```

Add the following line to your ESLint configuration file’s `extends` section:

```json
{
  "extends": ["plugin:chai-friendly/recommended"]
}
```

### Example ESLint Configuration

```javascript
module.exports = {
  env: {
    browser: true,
    es2021: true,
  },
  extends: ["airbnb-base", "plugin:chai-friendly/recommended"],
  parser: "@typescript-eslint/parser",
  parserOptions: {
    ecmaVersion: "latest",
    sourceType: "module",
  },
  plugins: ["@typescript-eslint"],
  rules: {
    "import/extensions": [
      "error",
      "ignorePackages",
      {
        js: "never",
        jsx: "never",
        ts: "never",
        tsx: "never",
      },
    ],
    "linebreak-style": 0,
  },
  settings: {
    "import/resolver": {
      node: {
        extensions: [".js", ".jsx", ".ts", ".tsx"],
      },
    },
  },
};
```

## Writing Tests

With this setup, it’s expected that the tests will be in the `tests` folder at the root of the application, with files ending in `.test.ts`. Thus, we will create the `tests` folder and a `users.test.ts` file for user-related tests.

First, we need to import the relevant testing modules and the app itself:

```ts
import request from "supertest";
import { expect } from "chai";
import { describe, it } from "mocha";
import app from "../app";
```

The `

request`module allows us to make requests to the application, while`expect`allows us to define various assertions to check if the application behaves as expected. The`describe`and`it` modules let us group and describe our tests.

Next, we can write a test that checks if creating a user works as expected. We will create an object containing the necessary data for user creation and send this object in the request body:

```ts
describe("Users controller", () => {
  describe("POST /users", () => {
    it("responds with user id and statusCode 201 after creating new user", async () => {
      const response = await request(app).post("/users").send(newUser);
      expect(response.body).to.be.a("object");
      expect(response.statusCode).to.equal(201);
      expect(response.body.success).to.be.true;
      expect(response.body.userId).to.be.a("number");
      expect(response.body.userId).to.equal(3); // Knowing that there are already two users in the test database, the new user's id should be 3
    });
  });
});
```

As seen in the example, we use the `describe` and `it` modules to group tests and describe their purpose. We then use the `request` module to send a request to the application with the `newUser` object in the body. Finally, we use `expect` and Chai assertions to check if the response is what we expect.

When we now run the test with `npm test`, we should see output similar to this:

```bash
  Users controller
    POST /users
      ✔ responds with user id and statusCode 201 after creating new user (116ms)

  1 passing (137ms)
```

Next, we can check if the user can log in and retrieve some data. For this, we need to send a request to the `POST /login` endpoint to receive the user's token, and then send a request to the `GET /users/:id` endpoint with the token. We can write a test like this:

```ts
let newUserToken: string; // Variable to store the token for future use
describe("POST /login", () => {
  it("responds with token and statusCode 200 for created user login", async () => {
    const response = await request(app).post("/login").send(newUser);
    expect(response.body).to.be.a("object");
    expect(response.statusCode).to.equal(200);
    expect(response.body.success).to.be.true;
    expect(response.body.token).to.be.a("string");
    newUserToken = response.body.token;
  });
});
describe("GET /users/:id", () => {
  it("responds with user object and statusCode 200 for user", async () => {
    const response = await request(app)
      .get("/users/3")
      .set("Authorization", `Bearer ${newUserToken}`);
    expect(response.body).to.deep.equal({
      success: true,
      message: "User",
      user: {
        id: 3,
        firstName: "Pille",
        lastName: "Piilupart",
        email: "pille@piilupart.ee",
        role: "User",
      },
    });
  });
});
```

The complete test file now looks like this:

```ts
/* eslint-disable import/no-unresolved */
/* eslint-disable import/extensions */
import request from "supertest";
import { expect } from "chai";
import { describe, it } from "mocha";
import app from "../src/app";

const newUser = {
  firstName: "Pille",
  lastName: "Piilupart",
  email: "pille@piilupart.ee",
  password: "pille",
};

let newUserToken: string;

describe("Users controller", () => {
  describe("POST /users", () => {
    it("responds with user id and statusCode 201 after creating new user", async () => {
      const response = await request(app).post("/users").send(newUser);
      expect(response.body).to.be.a("object");
      expect(response.statusCode).to.equal(201);
      expect(response.body.success).to.be.true;
      expect(response.body.userId).to.be.a("number");
      expect(response.body.userId).to.equal(3);
    });
  });
  describe("POST /login", () => {
    it("responds with token and statusCode 200 for created user login", async () => {
      const response = await request(app).post("/login").send(newUser);
      expect(response.body).to.be.a("object");
      expect(response.statusCode).to.equal(200);
      expect(response.body.success).to.be.true;
      expect(response.body.token).to.be.a("string");
      newUserToken = response.body.token;
    });
  });
  describe("GET /users/:id", () => {
    it("responds with user object and statusCode 200 for user", async () => {
      const response = await request(app)
        .get("/users/3")
        .set("Authorization", `Bearer ${newUserToken}`);
      expect(response.body).to.deep.equal({
        success: true,
        message: "User",
        user: {
          id: 3,
          firstName: "Pille",
          lastName: "Piilupart",
          email: "pille@piilupart.ee",
          role: "User",
        },
      });
    });
  });
});
```

Similarly, we can write tests for other use cases, such as:

- User creation fails when the user already exists.
- User creation fails when the user data is invalid.
- User creation fails when the user data is incomplete.
- Data retrieval fails when the user is not logged in.
- Data retrieval fails when the user does not exist.
- Data retrieval fails when the user is not an admin.
- ...

We can also write tests for other endpoints.

## Generating Coverage Reports

Once we have written our tests, it is useful to know how much of our application is covered by the tests. For this, we have several options, but one option is to use the [nyc](https://www.npmjs.com/package/nyc) module.

To install the `nyc` module:

```bash
npm install nyc
```

Next, we can add a new script to the `package.json` file:

```json
{
  "scripts": {
    "pretest": "ts-node ./scripts/create-test-db.js",
    "test": "cross-env NODE_ENV=test mocha -r ts-node/register 'tests/*.test.ts' --exit",
    "coverage": "nyc npm test"
  }
}
```

To see the coverage report, we can run the command `npm run coverage`. This will display a coverage report after the tests have been run, looking something like this:

```bash
--------------------------|---------|----------|---------|---------|-------------------
File                      | % Stmts | % Branch | % Funcs | % Lines | Uncovered Line #s
--------------------------|---------|----------|---------|---------|-------------------
All files                 |    73.6 |    51.78 |   47.27 |   74.71 |
 src                      |   94.64 |       75 |     100 |   94.64 |
  app.ts                  |     100 |      100 |     100 |     100 |
  config.ts               |     100 |      100 |     100 |     100 |
  createDatabase.ts       |   85.71 |      100 |     100 |   85.71 | 21,34-35
  database.ts             |     100 |       50 |     100 |     100 | 4
  db.ts                   |     100 |      100 |     100 |     100 |
 src/components/auth      |   88.88 |       75 |     100 |   88.88 |
  authControllers.ts      |   88.88 |       75 |     100 |   88.88 | 10,27
 src/components/helpers   |   78.57 |        0 |      70 |   78.57 |
  CustomError.ts          |      25 |      100 |       0 |      25 | 4-6
  errorFactory.ts         |      60 |        0 |       0 |      60 | 5-8
  hashServices.ts         |     100 |      100 |     100 |     100 |
  jwtServices.ts          |    90.9 |      100 |     100 |    90.9 | 16
 src/components/homeworks |      24 |        0 |       0 |   26.08 |
  homeworksControllers.ts |   23.07 |        0 |       0 |   23.07 | 6-35
  homeworksServices.ts    |      25 |        0 |       0 |      30 | 6-30
 src/components/logger    |      60 |      100 |       0 |      60 |
  loggerControllers.ts    |      60 |      100 |       0 |      60 | 6-7
  loggerServices.ts       |      60 |      100 |       0 |      60 | 5-7
 src/components/statuses  |      40 |      100 |       0 |   42.85 |
  statusesControllers.ts  |    37.5 |      100 |       0 |

    37.5 | 6-17
  statusesServices.ts     |   42.85 |      100 |       0 |      50 | 5-8
 src/components/subjects  |   43.33 |        0 |       0 |   44.82 |
  subjectsControllers.ts  |   23.07 |      100 |       0 |   23.07 | 6-34
  subjectsRoutes.ts       |     100 |      100 |     100 |     100 |
  subjectsServices.ts     |      30 |      100 |       0 |   33.33 | 5-23
 src/components/users     |   92.85 |    78.57 |     100 |   92.85 |
  usersControllers.ts     |      88 |    78.57 |     100 |      88 | 11,14,43
  usersRoutes.ts          |     100 |      100 |     100 |     100 |
  usersServices.ts        |   95.23 |      100 |     100 |   95.23 | 13
 src/middlewares          |   77.41 |    64.28 |      40 |   77.41 |
  errorMiddleware.ts      |      50 |        0 |       0 |      50 | 5-6
  isAdmin.ts              |     100 |      100 |     100 |     100 |
  isLoggedInMiddleware.ts |    90.9 |     87.5 |     100 |    90.9 | 14
  loggingMiddleware.ts    |      50 |      100 |       0 |      50 | 5-7
  notFoundMiddleware.ts   |      75 |      100 |       0 |      75 | 5
--------------------------|---------|----------|---------|---------|-------------------
```

The report provides a good overview of which files have been tested and to what extent. It also shows which lines are covered by tests and which are not.
