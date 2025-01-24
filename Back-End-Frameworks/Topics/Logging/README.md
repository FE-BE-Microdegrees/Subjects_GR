---
marp: true

---
# Σύνδεση σε μια εφαρμογή Express

Η καταγραφή της χρήσης του API είναι απαραίτητη για να κατανοήσετε πώς και πότε οι χρήστες αλληλεπιδρούν με το API σας. Η καταγραφή βοηθά στον εντοπισμό μοτίβων, στην παρακολούθηση των επιδόσεων και στη διάγνωση προβλημάτων. Στην Express, μπορείτε να υλοποιήσετε την καταγραφή με διάφορους τρόπους, χρησιμοποιώντας είτε ενσωματωμένες λειτουργίες είτε βιβλιοθήκες τρίτων. Μία από τις πιο δημοφιλείς και ισχυρές βιβλιοθήκες καταγραφής είναι η `winston`. Επιπλέον, μπορεί επίσης να χρησιμοποιηθεί η `morgan`, ένας απλός καταγραφέας αιτήσεων HTTP.


- [Σύνδεση σε μια εφαρμογή Express](#Σύνδεση-σε-μια-εφαρμογή-Express)
  - [Μαθησιακά αποτελέσματα](#Μαθησιακά-αποτελέσματα)
  - [Εγκατάσταση](#Εγκατάσταση)
  - [1. Morgan: Καταγραφή αιτημάτων HTTP](#1-Morgan-Καταγραφή-αιτημάτων-HTTP)
    - [Χρησιμοποιώντας τη Morgan](#Χρησιμοποιώντας-τη-Morgan)
    - [Μορφές καταγραφής Morgan](#Μορφές-καταγραφής-Morgan)
    - [Αποθήκευση αρχείων καταγραφής σε αρχείο](#Αποθήκευση-αρχείων-καταγραφής-σε-αρχείο)
  - [2. Winston: Προηγμένη καταγραφή](#2-Winston-Προηγμένη-καταγραφή)
    - [Ρύθμιση της Winston](#Ρύθμιση-της-Winston)
    - [Ενσωμάτωση του Winston με την Express](#Ενσωμάτωση-του-Winston-με-την-Express)
    - [Επεξήγηση](#Επεξήγηση)
  - [Επίπεδα καταγραφής](#Επίπεδα καταγραφής)

## Μαθησιακά αποτελέσματα

Στο τέλος αυτού του υλικού, οι εκπαιδευόμενοι θα πρέπει να είναι σε θέση να:

- να εξηγούν τη σημασία της καταγραφής της χρήσης του API,
- να εγκαθιστούν και να ρυθμίζουν τις βιβλιοθήκες καταγραφής `morgan` και `winston`,
- να υλοποιούν την καταγραφή χρήσης API στην Express χρησιμοποιώντας τις βιβλιοθήκες `morgan` και `winston`,
- να καταγράφουν λεπτομέρειες αιτήσεων και σφαλμάτων για μεταγενέστερη ανάλυση.

## Εγκατάσταση

Αρχικά, εγκαταστήστε τις απαιτούμενες βιβλιοθήκες:

```bash
npm install morgan winston
```

## 1. **Morgan: Καταγραφή αιτημάτων HTTP**

Το `morgan` είναι μια βιβλιοθήκη καταγραφής αιτημάτων HTTP που μπορεί εύκολα να ενσωματωθεί σε μια εφαρμογή Express.

### Χρησιμοποιώντας τη Morgan

Προσθέστε το `morgan` στην εφαρμογή Express για να καταγράφετε όλες τις εισερχόμενες αιτήσεις HTTP.

```javascript
// app.js
const express = require('express');
const morgan = require('morgan');
const bodyParser = require('body-parser');
const usersRouter = require('./routes/users');

const app = express();

// Morgan logs all requests
app.use(morgan('combined')); // You can choose different log formats (dev, combined, tiny, etc.)

app.use(bodyParser.json());
app.use('/users', usersRouter);

// If no route matches
app.use((req, res, next) => {
  res.status(404).json({
    success: false,
    message: 'Resource not found',
  });
});

// Central error handler
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(err.status || 500).json({
    success: false,
    message: err.message || 'Internal Server Error',
  });
});

module.exports = app;

```

### Μορφές καταγραφής Morgan

Το `morgan` προσφέρει διάφορες μορφές καταγραφής:

- **combined**: Λεπτομερή αρχεία καταγραφής με πολλές πληροφορίες (καλό για την παραγωγή).
- **common**: Γενική μορφή αρχείου καταγραφής.
- **dev**: Σύντομη και πολύχρωμη μορφή ημερολογίου (καλή για ανάπτυξη).
- **short**: Σύντομη μορφή αρχείου καταγραφής.
- **tiny**: Πολύ σύντομη μορφή ημερολογίου.

### Αποθήκευση αρχείων καταγραφής σε αρχείο

Αν θέλετε να αποθηκεύσετε τα αρχεία καταγραφής σε ένα αρχείο για μεταγενέστερη ανάλυση, μπορείτε να χρησιμοποιήσετε το `morgan` με την ενότητα `fs`.

```javascript
const fs = require('fs');
const path = require('path');

// Log file stream
const accessLogStream = fs.createWriteStream(path.join(__dirname, 'access.log'), { flags: 'a' });

// Use 'combined' format and save logs to a file
app.use(morgan('combined', { stream: accessLogStream }));

```

## 2. Winston: Προηγμένη καταγραφή

Η `winston` είναι μια ευέλικτη και ισχυρή βιβλιοθήκη καταγραφής που μπορεί να χρησιμοποιηθεί για διαφορετικά επίπεδα και μορφές καταγραφής.

### Ρύθμιση της Winston

Δημιουργήστε έναν καταγραφέα `winston` και ενσωματώστε τον στην εφαρμογή Express.

```javascript
// logger.js
const { createLogger, format, transports } = require('winston');
const { combine, timestamp, printf, errors } = format;

// Custom log format
const logFormat = printf(({ level, message, timestamp, stack }) => {
  return `${timestamp} ${level}: ${stack || message}`;
});

const logger = createLogger({
  level: 'info',
  format: combine(
    timestamp(),
    errors({ stack: true }), // Log errors with stack trace
    logFormat
  ),
  transports: [
    new transports.Console(),
    new transports.File({ filename: 'combined.log' }),
    new transports.File({ filename: 'errors.log', level: 'error' }),
  ],
});

module.exports = logger;

```

### Ενσωμάτωση του Winston με την Express

Χρησιμοποιήστε τον καταγραφέα `winston` στην εφαρμογή Express για να καταγράφετε αιτήσεις και σφάλματα HTTP.

```javascript
// app.js
const express = require('express');
const morgan = require('morgan');
const bodyParser = require('body-parser');
const usersRouter = require('./routes/users');
const logger = require('./logger');

const app = express();

// Morgan logs all requests, using winston
app.use(morgan('combined', { stream: { write: message => logger.info(message.trim()) }}));

app.use(bodyParser.json());
app.use('/users', usersRouter);

// If no route matches
app.use((req, res, next) => {
  res.status(404).json({
    success: false,
    message: 'Resource not found',
  });
});

// Central error handler
app.use((err, req, res, next) => {
  logger.error(err.message, { stack: err.stack });
  res.status(err.status || 500).json({
    success: false,
    message: err.message || 'Internal Server Error',
  });
});

module.exports = app;

```

### Επεξήγηση

- **Using Morgan and Winston Together**: Χρησιμοποιούμε τη βιβλιοθήκη καταγραφής `morgan` με το `winston` για να καταγράφουμε λεπτομερώς τις αιτήσεις HTTP και να τις αποθηκεύουμε σε ένα αρχείο.
- **Custom Log Format**: Το `winston` επιτρέπει τον ορισμό μιας προσαρμοσμένης μορφής καταγραφής που περιλαμβάνει χρονοσφραγίδες και μηνύματα σφάλματος με ίχνη στοίβας.
- **Central Error Handler**: Καταγράφουμε τα σφάλματα χρησιμοποιώντας τον καταγραφέα `winston`, ο οποίος βοηθά στην ανάλυση των σφαλμάτων αργότερα.
  
## Επίπεδα καταγραφής

Το `winston` έχει διαφορετικά επίπεδα καταγραφής, τα οποία βοηθούν στην κατηγοριοποίηση και το φιλτράρισμα των αρχείων καταγραφής:

- **error**: Μηνύματα σφάλματος.
- **warn**: Προειδοποιήσεις.
- **info**: Ενημερωτικά μηνύματα.
- **http**: Καταγραφή αιτήσεων HTTP.
- **verbose**: Πιο λεπτομερή μηνύματα.
- **debug**: Μηνύματα αποσφαλμάτωσης SD.
- **silly**: Πολύ λεπτομερή μηνύματα.
