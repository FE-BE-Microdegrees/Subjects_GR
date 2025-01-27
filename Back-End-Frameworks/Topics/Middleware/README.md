 # Middleware στην Express

Σε αυτή την ενότητα, θα συζητήσουμε το middleware στο πλαίσιο της Express.js.


- [Middleware στην Express](#Middleware-στην-Express)
  - [Μαθησιακά αποτελέσματα](#Μαθησιακά-αποτελέσματα)
  - [Τι είναι οι συναρτήσεις Middleware;](#Τι-είναι-οι-λειτουργίες-Middleware)
  - [Next Function](#next-function)
  - [Χρήση Middleware](#Χρήση-Middleware)
    - [Παράδειγμα Logging Middleware](#Παράδειγμα-logging-middleware)
  - [Κύκλος αιτήματος/απάντησης με Middleware](#Κύκλος-αιτήματος-απάντησης-με-Middleware)
  - [Not Found Middleware](#not-found-middleware)
    - [Καταχώριση Not Found Middleware](#Καταχώριση-not-found-middleware)

## Μαθησιακά αποτελέσματα

Στο τέλος αυτής της ενότητας, θα είστε σε θέση να:

- Να εξηγείτε τι είναι το middleware και πώς χρησιμοποιείται.
- Να γράφετε συναρτήσεις middleware.
- Να υλοποιείτε middleware σε μια εφαρμογή Express.js.

## Τι είναι οι συναρτήσεις Middleware;

Οι συναρτήσεις middleware είναι συναρτήσεις που έχουν πρόσβαση στο αντικείμενο αίτησης (`req`), στο αντικείμενο απόκρισης (`res`) και στην επόμενη συνάρτηση middleware στον κύκλο αίτησης-απόκρισης της εφαρμογής. Ουσιαστικά, μπορείτε να σκεφτείτε το middleware ως ένα φίλτρο που επεξεργάζεται τις αιτήσεις πριν φτάσουν στο επόμενο στάδιο του κύκλου αίτησης-απόκρισης. Για παράδειγμα, το middleware θα μπορούσε να χειριστεί την καταγραφή, τον έλεγχο ταυτότητας, την ανάλυση δεδομένων αιτήσεων ή οποιαδήποτε άλλη λειτουργικότητα που είναι σημαντική για την εφαρμογή.

## Next Function

Η συνάρτηση `next` είναι μια συνάρτηση δρομολόγησης Express που, όταν καλείται, μεταβιβάζει τον έλεγχο στο επόμενο middleware της στοίβας.

## Χρήση Middleware

Το Middleware μπορεί:

- Να εκτελεί κώδικα.
- Να τροποποιεί τα αντικείμενα αίτησης και απόκρισης.
- Να τερματίσει τον κύκλο αίτησης-απάντησης.
- Να καλέσει το επόμενο middleware στη στοίβα.
  
Είναι σημαντικό να θυμάστε ότι αν ένα ενδιάμεσο λογισμικό δεν τερματίσει τον κύκλο αίτησης-απάντησης (π.χ. χρησιμοποιώντας `return res.status(200).json...`), πρέπει να καλέσει τη συνάρτηση `next()`, διαφορετικά η εφαρμογή θα κολλήσει.

### Παράδειγμα Logging Middleware

```javascript
// Middleware for logging HTTP requests

const logger = (req, res, next) => {
  // Log the request URL, method, and time
  console.log(req.url, req.method, new Date().toISOString());
  // Call the next middleware
  return next();
};
```

Το ενδιάμεσο λογισμικό μπορεί να εφαρμοστεί με διάφορους τρόπους.

Μια επιλογή είναι η καταχώρηση του ενδιάμεσου λογισμικού για όλες τις αιτήσεις:

```javascript
...
// Importing middleware (path depends on file location)
const logger = require('./middlewares/logger');

...

// Registering middleware
app.use(logger);

...
```

Μια άλλη επιλογή είναι η καταχώριση ενδιάμεσου λογισμικού μόνο για συγκεκριμένες διαδρομές:


```javascript
...
// Importing middleware
const logger = require('./middlewares/logger');

...

// Registering middleware
app.get('/api', logger, (req, res) => {
  res.send('Hello World!');
});
...
```

## Κύκλος αιτήματος/απάντησης με Middleware


## Not Found Middleware

Ένα χρήσιμο σενάριο για το ενδιάμεσο λογισμικό είναι η εμφάνιση μιας σελίδας 404 όταν ο ζητούμενος πόρος δεν βρέθηκε. Παράδειγμα:

```javascript
// Middleware to display a 404 page when the requested resource is not found

const notFound = (req, res, next) => {
  res.status(404).send({
    success: false,
    message: "Route not found",
  });
};

module.exports = notFound;
```

### Καταχώριση Not Found Middleware

```javascript
...
// Importing middleware
const notFound = require('./middlewares/notFound');

...

// Registering middleware
app.use('*', notFound);

...
```
Εδώ, είναι σημαντικό να καταχωρήσετε αυτό το ενδιάμεσο λογισμικό μετά από όλες τις διαδρομές, χρησιμοποιώντας τη διαδρομή `*`. Αυτό σημαίνει ότι αν ένας χρήστης έχει πρόσβαση σε μια διαδρομή που δεν υπάρχει στο API, θα οδηγηθεί σε αυτή τη λειτουργία middleware.

Τώρα, αν ένας χρήστης προσπαθήσει να αποκτήσει πρόσβαση σε μια διαδρομή που δεν υπάρχει, θα λάβει την ακόλουθη απάντηση:

```json
{
  "success": false,
  "message": "Route not found"
}
```
