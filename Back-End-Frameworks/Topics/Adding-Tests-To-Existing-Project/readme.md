# Πώς να προσθέσετε δοκιμές σε ένα υπάρχον API Node Express;

Σε αυτή την ενότητα, θα εξερευνήσουμε τον τρόπο δημιουργίας αυτοματοποιημένων δοκιμών End-to-End για ένα υπάρχον API Node.js Express.

Θα χρησιμοποιήσουμε το πλαίσιο δοκιμών [Mocha](../mocha/README.md), την ενότητα [Supertest](../supertest/README.md) και τους ισχυρισμούς [Chai](../chai/README.md).

## Μαθησιακά αποτελέσματα

Στο τέλος αυτής της ενότητας, οι μαθητές θα πρέπει να είναι σε θέση να:

- Να δημιουργούν δοκιμές για ένα υπάρχον Node.js Express API.
- Να χρησιμοποιούν το πλαίσιο δοκιμών Mocha.
- Να χρησιμοποιούν την ενότητα Supertest.
- Να χρησιμοποιούν τους ισχυρισμούς Chai.
- Να δημιουργούν αναφορές κάλυψης για τις δοκιμές.
- Χρησιμοποιήστε μια βάση δεδομένων δοκιμών κατά τη συγγραφή δοκιμών.
- Διαχωρίστε τη λογική της εφαρμογής από την εκκίνηση του διακομιστή.
- Δομήστε μια εφαρμογή για τη συγγραφή δοκιμών.

## Δομή της εφαρμογής

Το πρώτο βήμα για την προσθήκη αυτοματοποιημένων δοκιμών στο υπάρχον Node.js Express API σας είναι να διαχωρίσετε την «εφαρμογή» Express από την αρχικοποίησή της. Αυτό είναι απαραίτητο ώστε να μπορούμε να χρησιμοποιήσουμε τη μεταβλητή `app` κατά τη διάρκεια των δοκιμών χωρίς να εκκινήσουμε απευθείας τον διακομιστή.

Για να το κάνουμε αυτό, θα αφαιρέσουμε τη λογική δημιουργίας της εφαρμογής από το υπάρχον αρχείο `index.ts` και θα αφήσουμε μόνο την εκκίνηση του διακομιστή. Αυτό σημαίνει ότι το αρχείο `index.ts` θα πρέπει να μοιάζει με αυτό:


```typescript
import app from "./app";

const port = process.env.PORT || 3000;

app.listen(port, () => {
  console.log(`Server running on port ${port}`);
});
```

Στη συνέχεια, θα δημιουργήσουμε ένα νέο αρχείο `app.ts`, όπου θα τοποθετήσουμε όλο τον κώδικα που σχετίζεται με τη δημιουργία της `app`. Αυτό σημαίνει ότι το αρχείο `app.ts` θα πρέπει να μοιάζει με αυτό:


```typescript
import express from "express";

const app = express();

app.use(express.json());

app.get("/", (_req, res) => {
  res.send("Hello World!");
});

export default app;
```

Με αυτή τη δομή, μπορούμε να εισάγουμε την εφαρμογή (`app`) στις δοκιμές μας και να τη χρησιμοποιήσουμε χωρίς να εκκινήσουμε τον διακομιστή.

## Δημιουργία δεδομένων δοκιμής και χρήση βάσης δεδομένων δοκιμής

Στη συνέχεια, πρέπει να καθορίσουμε πώς θα λάβουμε τα δεδομένα που απαιτούνται για τη δοκιμή της εφαρμογής μας. Δεδομένου ότι ο στόχος μας είναι να δοκιμάσουμε την εφαρμογή όπως θα χρησιμοποιούνταν στην παραγωγή, θέλουμε να διασφαλίσουμε ότι αλληλεπιδρά σωστά με τη βάση δεδομένων.

Για να λάβουμε τα απαραίτητα δεδομένα για τις δοκιμές, έχουμε διάφορες επιλογές:

- Χρησιμοποιήστε την υπάρχουσα ζωντανή βάση δεδομένων.
- Δημιουργήστε μια νέα βάση δεδομένων.
- Χρησιμοποιήστε μια βάση δεδομένων στη μνήμη αντί για μια πραγματική βάση δεδομένων.
- Χρησιμοποιήστε μια εικονική βάση δεδομένων αντί για μια πραγματική βάση δεδομένων.

Η χρήση της υπάρχουσας βάσης δεδομένων έχει σημαντικά μειονεκτήματα, όπως η μόλυνσή της με δεδομένα δοκιμών και η μη δυνατότητα να εγγυηθεί ότι τα δεδομένα βρίσκονται στην αναμενόμενη κατάσταση.

Για να αποφύγουμε αυτά τα ζητήματα, πρέπει να δημιουργήσουμε μια νέα βάση δεδομένων για δοκιμές.

### Αυτοματοποίηση δημιουργίας βάσης δεδομένων

Για να αυτοματοποιήσουμε τη δημιουργία μιας νέας βάσης δεδομένων, θα γράψουμε ένα ξεχωριστό σενάριο που θα δημιουργεί τη βάση δεδομένων και θα εισάγει τα απαραίτητα δεδομένα.

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

Αυτό το σενάριο απαιτεί ένα αρχείο `init.sql` που περιέχει τις απαραίτητες εντολές SQL για τη ρύθμιση της βάσης δεδομένων. Για παράδειγμα, το αρχείο `init.sql` μπορεί να μοιάζει ως εξής:

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

Τώρα μπορούμε να εκτελέσουμε αυτό το σενάριο πριν από την εκτέλεση των δοκιμών μας προσθέτοντας ένα νέο σενάριο στο αρχείο `package.json`:

```json
{
  "scripts": {
    "pretest": "ts-node ./scripts/create-test-db.js"
  }
}
```

Το σενάριο `pretest` εξασφαλίζει ότι το σενάριο εγκατάστασης της βάσης δεδομένων εκτελείται πριν από τις δοκιμές.

Στη συνέχεια, πρέπει να διασφαλίσουμε ότι όταν εκτελούμε τις δοκιμές μας, χρησιμοποιείται η βάση δεδομένων των δοκιμών. Ένας τρόπος για να το πετύχουμε αυτό είναι να χρησιμοποιήσουμε μια μεταβλητή περιβάλλοντος για να ενημερώσουμε την εφαρμογή ποια βάση δεδομένων να χρησιμοποιήσει. Για να το κάνουμε αυτό, θα τροποποιήσουμε το αρχείο ρυθμίσεων της βάσης δεδομένων ώστε να επιλέγει την κατάλληλη βάση δεδομένων με βάση τη μεταβλητή περιβάλλοντος.

Το αρχείο μας `config.ts` μπορεί να μοιάζει ως εξής:

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

Στη συνέχεια, πρέπει να προσθέσουμε μια λειτουργικότητα για να διαβάζουμε τη μεταβλητή περιβάλλοντος και να επιστρέφουμε την κατάλληλη διαμόρφωση της βάσης δεδομένων. Αυτό θα μπορούσε να μοιάζει με:


```ts
import mysql2 from "mysql2";
import config from "./config";

const dbConfig = config.db[process.env.NODE_ENV || "development"];

const db = mysql2.createConnection(dbConfig).promise();

export default db;
```

Αν η TypeScript δώσει σφάλμα για το `process.env.NODE_ENV`, μπορούμε να ορίσουμε μια διασύνδεση για τη διαμόρφωση που επιτρέπει οποιοδήποτε κλειδί συμβολοσειράς αλλά απαιτεί η τιμή να είναι ένα αντικείμενο διαμόρφωσης της βάσης δεδομένων.

### Παράδειγμα Configuration Interface

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

Είναι επίσης σκόπιμο να ορίσετε μια διεπαφή για ολόκληρο το αρχείο `config.ts`:

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

Στη συνέχεια, πρέπει να διασφαλίσουμε ότι οι δοκιμές εκτελούνται στο σωστό περιβάλλον. Ένας τρόπος για να γίνει αυτό είναι η χρήση της ενότητας `cross-env`. Πρώτα, εγκαθιστούμε το `cross-env`:

```bash
npm install cross-env
```

Στη συνέχεια, μπορούμε να προσθέσουμε τη μεταβλητή περιβάλλοντος στο αρχείο `package.json`:


```json
{
  "scripts": {
    "pretest": "ts-node ./scripts/create-test-db.js",
    "test": "cross-env NODE_ENV=test mocha -r ts-node/register 'tests/*.test.ts' --exit"
  }
}
```

Τώρα, όταν εκτελούμε το `npm test`, το σενάριο για τη δημιουργία της δοκιμαστικής βάσης δεδομένων θα εκτελεστεί πριν από την εκτέλεση των δοκιμών.

## Εγκαθιστώντας το Testing Frameworks

Στη συνέχεια, πρέπει να εγκαταστήσουμε τα απαραίτητα πλαίσια και τους ορισμούς τύπων για τη συγγραφή δοκιμών. Θα εγκαταστήσουμε τα [Mocha](../mocha/README.md), [Supertest](../supertest/README.md) και [Chai](../chai/README.md):

```bash
npm install mocha supertest chai
npm install -D @types/mocha @types/supertest @types/chai
```

Επιπλέον, πρέπει να ενημερώσουμε τη ρύθμιση παραμέτρων του ESLint για να αποφύγουμε τις προειδοποιήσεις σχετικά με τους ισχυρισμούς Chai. Πρώτον, πρέπει να εγκαταστήσουμε την ενότητα `eslint-plugin-chai-friendly`:

```bash
npm install eslint-plugin-chai-friendly --save-dev
```

Προσθέστε την ακόλουθη γραμμή στην ενότητα `extends` του αρχείου ρυθμίσεων ESLint:

```json
{
  "extends": ["plugin:chai-friendly/recommended"]
}
```

###  Παράδειγμα ESLint Configuration

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

Με αυτή τη ρύθμιση, αναμένεται ότι οι δοκιμές θα βρίσκονται στο φάκελο `tests` στη ρίζα της εφαρμογής, με τα αρχεία να τελειώνουν σε `.test.ts`. Έτσι, θα δημιουργήσουμε το φάκελο `tests` και ένα αρχείο `users.test.ts` για τις δοκιμές που σχετίζονται με τους χρήστες.

Πρώτα, πρέπει να εισάγουμε τις σχετικές ενότητες δοκιμών και την ίδια την εφαρμογή:


```ts
import request from "supertest";
import { expect } from "chai";
import { describe, it } from "mocha";
import app from "../app";
```

Η ενότητα `request` μας επιτρέπει να κάνουμε αιτήσεις στην εφαρμογή, ενώ η ενότητα `expect` μας επιτρέπει να ορίσουμε διάφορους ισχυρισμούς για να ελέγξουμε αν η εφαρμογή συμπεριφέρεται όπως αναμένεται. Οι ενότητες `describe`και `it` μας επιτρέπουν να ομαδοποιήσουμε και να περιγράψουμε τις δοκιμές μας.

Στη συνέχεια, μπορούμε να γράψουμε μια δοκιμή που ελέγχει αν η δημιουργία ενός χρήστη λειτουργεί όπως αναμένεται. Θα δημιουργήσουμε ένα αντικείμενο που θα περιέχει τα απαραίτητα δεδομένα για τη δημιουργία χρήστη και θα στείλουμε αυτό το αντικείμενο στο σώμα της αίτησης:

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

Όπως φαίνεται στο παράδειγμα, χρησιμοποιούμε τις ενότητες `describe` και `it` για να ομαδοποιήσουμε τις δοκιμές και να περιγράψουμε το σκοπό τους. Στη συνέχεια χρησιμοποιούμε την ενότητα `request` για να στείλουμε μια αίτηση στην εφαρμογή με το αντικείμενο `newUser` στο σώμα. Τέλος, χρησιμοποιούμε τα `expect` και τους ισχυρισμούς Chai για να ελέγξουμε αν η απάντηση είναι αυτή που περιμένουμε.

Όταν τώρα εκτελέσουμε τη δοκιμή με το `npm test`, θα πρέπει να δούμε έξοδο παρόμοια με αυτή:


```bash
  Users controller
    POST /users
      ✔ responds with user id and statusCode 201 after creating new user (116ms)

  1 passing (137ms)
```

Στη συνέχεια, μπορούμε να ελέγξουμε αν ο χρήστης μπορεί να συνδεθεί και να ανακτήσει κάποια δεδομένα. Για το σκοπό αυτό, πρέπει να στείλουμε ένα αίτημα στο τελικό σημείο `POST /login` για να λάβουμε το token του χρήστη και στη συνέχεια να στείλουμε ένα αίτημα στο τελικό σημείο `GET /users/:id` με το token. Μπορούμε να γράψουμε μια δοκιμή ως εξής:


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

Το πλήρες αρχείο δοκιμής μοιάζει τώρα ως εξής:

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

Ομοίως, μπορούμε να γράψουμε δοκιμές για άλλες περιπτώσεις χρήσης, όπως:

- Η δημιουργία χρήστη αποτυγχάνει όταν ο χρήστης υπάρχει ήδη.
- Η δημιουργία χρήστη αποτυγχάνει όταν τα δεδομένα του χρήστη είναι άκυρα.
- Η δημιουργία χρήστη αποτυγχάνει όταν τα δεδομένα χρήστη είναι ελλιπή.
- Η ανάκτηση δεδομένων αποτυγχάνει όταν ο χρήστης δεν είναι συνδεδεμένος.
- Η ανάκτηση δεδομένων αποτυγχάνει όταν ο χρήστης δεν υπάρχει.
- Η ανάκτηση δεδομένων αποτυγχάνει όταν ο χρήστης δεν είναι διαχειριστής.
- ...

Μπορούμε επίσης να γράψουμε δοκιμές για άλλα τελικά σημεία.

## Δημιουργία Coverage Reports

Αφού γράψουμε τις δοκιμές μας, είναι χρήσιμο να γνωρίζουμε πόσο μεγάλο μέρος της εφαρμογής μας καλύπτεται από τις δοκιμές. Για το σκοπό αυτό, έχουμε διάφορες επιλογές, αλλά μια επιλογή είναι να χρησιμοποιήσουμε την ενότητα [nyc](https://www.npmjs.com/package/nyc).

Για να εγκαταστήσετε την ενότητα `nyc`:

```bash
npm install nyc
```

Στη συνέχεια, μπορούμε να προσθέσουμε ένα νέο σενάριο στο αρχείο `package.json`:


```json
{
  "scripts": {
    "pretest": "ts-node ./scripts/create-test-db.js",
    "test": "cross-env NODE_ENV=test mocha -r ts-node/register 'tests/*.test.ts' --exit",
    "coverage": "nyc npm test"
  }
}
```

Για να δούμε την αναφορά κάλυψης, μπορούμε να εκτελέσουμε την εντολή `npm run coverage`. Αυτό θα εμφανίσει μια αναφορά κάλυψης μετά την εκτέλεση των δοκιμών, η οποία θα μοιάζει κάπως έτσι:

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

Η έκθεση παρέχει μια καλή επισκόπηση των αρχείων που έχουν δοκιμαστεί και σε ποιο βαθμό. Δείχνει επίσης ποιες γραμμές καλύπτονται από δοκιμές και ποιες όχι.

