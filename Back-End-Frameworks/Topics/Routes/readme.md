# Χρήση Router στο Express Framework

Σε αυτή την ενότητα, θα συζητήσουμε τον `Router` στο πλαίσιο Express.js.


- [Χρήση Router στο Express Framework](#Χρήση-Router-στο-Express-Framework)
  - [Μαθησιακά αποτελέσματα](#Μαθησιακά-αποτελέσματα)
  - [Router](#router)
  - [Δημιουργία ενός Router](#Δημιουργία-ενός-Router)
  - [Χρήση Middleware με δρομολογητές](#Χρήση-Middleware-με-δρομολογητές)
  - [Συμπέρασμα](#Συμπέρασμα)

## Μαθησιακά αποτελέσματα

Στο τέλος αυτής της ενότητας, θα είστε σε θέση να:

- Να εξηγείτε τι είναι ο «δρομολογητής» και πώς χρησιμοποιείται.
- Να δημιουργείτε `Router` σε μια εφαρμογή Express.js.
- Να χρησιμοποιείτε `Router`s για την ομαδοποίηση διαδρομών.

Μέχρι στιγμής, είχαμε διαφορετικές διαδρομές ορισμένες απευθείας στο αρχείο `app.js`. Ωστόσο, καθώς αυξάνεται ο αριθμός των διαδρομών, το περιεχόμενο του αρχείου μπορεί να γίνει πολύ μεγάλο και δύσκολο να διαβαστεί. Για να δομήσουμε καλύτερα τον κώδικα και να κάνουμε το αρχείο `app.js` πιο ευανάγνωστο, μπορούμε να χρησιμοποιήσουμε τον `express Router`.

## Router

Το `Router` είναι ένα αντικείμενο στο πλαίσιο `Express` που μας επιτρέπει να ομαδοποιούμε διαδρομές. Για παράδειγμα, αν χρειαζόμαστε ξεχωριστές διαδρομές για χρήστες και για αναρτήσεις, μπορούμε να τις τοποθετήσουμε σε ξεχωριστά `Router`.

Επί του παρόντος, αν το αρχείο `app.js` έχει διαδρομές που ορίζονται ως εξής:

```javascript
app.get("/logs", logger, loggerControllers.getLogs);
app.post("/login", authControllers.login);
app.post("/users", usersControllers.createUser);
app.use(isLoggedInMiddleware);
app.get("/users", isAdmin, usersControllers.getUsers);
app.get("/users/:id", usersControllers.getUserById);
app.get("/statuses", statusesControllers.getStatuses);
app.get("/statuses/:id", statusesControllers.getStatusById);
app.get("/subjects", subjectsControllers.getSubjects);
app.get("/subjects/:id", subjectsControllers.getSubjectById);
app.post("/subjects", subjectsControllers.createSubject);
app.get("/homeworks", homeworksControllers.getHomeworks);
app.get("/homeworks/:id", homeworksControllers.getHomeworkById);
app.post("/homeworks", homeworksControllers.createHomework);
```

Βλέπουμε ότι οι διαδρομές αυτές σχηματίζουν ήδη ομάδες ανάλογα με τους πόρους. Για παράδειγμα, έχουμε διαδρομές που αφορούν τους χρήστες, διαδρομές που σχετίζονται με το θέμα και διαδρομές που σχετίζονται με την εργασία στο σπίτι. Τώρα μπορούμε να μετακινήσουμε αυτές τις ομάδες σε ξεχωριστά `Router`.

## Δημιουργία ενός Router

Αρχικά, δημιουργήστε ένα νέο αρχείο στον αντίστοιχο φάκελο συστατικών που θα περιέχει τις διαδρομές που σχετίζονται με αυτόν τον πόρο. Για παράδειγμα, οι διαδρομές που σχετίζονται με τα θέματα θα μπορούσαν να βρίσκονται σε ένα αρχείο με όνομα `subjectsRoutes.js`. Πρώτον, εισαγάγετε την `express` σε αυτό το αρχείο:

```javascript
const express = require("express");
```

Then, we can create a `Router` object:

```javascript
const router = express.Router();
```

Επιπλέον, θα πρέπει να εισάγουμε τους αντίστοιχους ελεγκτές που θα χρησιμοποιούν οι διαδρομές:

```javascript
const subjectsControllers = require("./subjectsControllers");
```

Στη συνέχεια, μετακινήστε όλες τις διαδρομές που σχετίζονται με το θέμα από το `app.js` στο `subjectsRoutes.js` και ξαναγράψτε τις ελαφρώς ώστε να χρησιμοποιούν το `router` αντί του `app`:

```javascript
router.get("/", subjectsControllers.getSubjects);
router.get("/:id", subjectsControllers.getSubjectById);
router.post("/", subjectsControllers.createSubject);
```

Τέλος, εξάγετε το `router` και εισάγετε το στο `app.js`:

```javascript
module.exports = router;
```

Στο αρχείο `app.js`, εισάγετε το αρχείο `subjectsRoutes.js` και χρησιμοποιήστε τη μέθοδο `app.use` για να ενημερώσετε την Express ότι έχουμε ένα τέτοιο `Router`:

```javascript
const subjectsRoutes = require("./subjects/subjectsRoutes");

app.use("/subjects", subjectsRoutes);
```

Το τελικό αρχείο `subjectsRoutes.js` θα μοιάζει με αυτό:

```javascript
const express = require("express");
const subjectsControllers = require("./subjectsControllers");

const router = express.Router();

router.get("/", subjectsControllers.getSubjects);
router.get("/:id", subjectsControllers.getSubjectById);
router.post("/", subjectsControllers.createSubject);

module.exports = router;
```

## Χρήση Middleware με δρομολογητές

Η χρήση middleware με το `Router` λειτουργεί όπως ακριβώς και με την `app`. Για παράδειγμα, αν πρέπει να χρησιμοποιήσουμε το `isLoggedInMiddleware`, μπορούμε να το κάνουμε ως εξής:

```javascript
const express = require("express");
const subjectsControllers = require("./subjectsControllers");
const isLoggedInMiddleware = require("../auth/isLoggedInMiddleware");

const router = express.Router();

router.get("/", isLoggedInMiddleware, subjectsControllers.getSubjects);

module.exports = router;
```

Είναι επίσης σημαντικό να θυμόμαστε ότι όταν χρησιμοποιούμε το `Router`, δεν μπορούμε να χρησιμοποιήσουμε τη μέθοδο `app.use` για να εφαρμόσουμε middleware για όλες τις διαδρομές. Αντ' αυτού, πρέπει να χρησιμοποιήσουμε τη μέθοδο `router.use`:


```javascript
const express = require("express");
const subjectsControllers = require("./subjectsControllers");
const isLoggedInMiddleware = require("../auth/isLoggedInMiddleware");

const router = express.Router();

router.use(isLoggedInMiddleware);

router.get("/subjects", subjectsControllers.getSubjects);

module.exports = router;
```

Εναλλακτικά, μπορούμε να καταχωρήσουμε το ενδιάμεσο λογισμικό στο αρχείο `app.js` πριν χρησιμοποιήσουμε τον αντίστοιχο `router`:

```javascript
const subjectsRoutes = require("./subjects/subjectsRoutes");

app.use(isLoggedInMiddleware);
app.use(subjectsRoutes);
```

## Συμπέρασμα

Οι «δρομολογητές» είναι πολύ χρήσιμοι όταν έχουμε πολλές διαδρομές και θέλουμε να τις ομαδοποιήσουμε. Κάνουν επίσης τον κώδικά μας πιο ευανάγνωστο και καλύτερα δομημένο. Επιπλέον, μπορούμε να χρησιμοποιήσουμε middleware στους `Router`s όπως ακριβώς κάνουμε και στην `app`.
