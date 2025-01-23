# Ανέβασμα και λήψη αρχείων

Το ανέβασμα και το κατέβασμα αρχείων στο Node.js με το Express μπορεί εύκολα να υλοποιηθεί χρησιμοποιώντας πλαίσια και ενότητες όπως το `multer` (για το ανέβασμα αρχείων) και το ίδιο το `express` (για το κατέβασμα αρχείων).

---

## Ανέβασμα αρχείου

### 1. **Εγκαταστήστε το `multer`**

Εκτελέστε την ακόλουθη εντολή για να εγκαταστήσετε το `multer`:

```bash
npm install multer
```
### 2. Δημιουργία ενός API για το ανέβασμα αρχείων
```javascript
// upload.js
const express = require('express');
const multer = require('multer');
const path = require('path');

const router = express.Router();

// Set storage engine
const storage = multer.diskStorage({
  destination: './uploads/',
  filename: function (req, file, cb) {
    cb(null, file.fieldname + '-' + Date.now() + path.extname(file.originalname));
  }
});

// Initialize upload
const upload = multer({
  storage: storage,
  limits: { fileSize: 1000000 }, // Limit: 1MB
  fileFilter: function (req, file, cb) {
    checkFileType(file, cb);
  }
}).single('myFile');

// Check File Type
function checkFileType(file, cb) {
  const filetypes = /jpeg|jpg|png|gif/; // Allowed extensions
  const extname = filetypes.test(path.extname(file.originalname).toLowerCase()); // Check extension
  const mimetype = filetypes.test(file.mimetype); // Check mime type

  if (mimetype && extname) {
    return cb(null, true);
  } else {
    cb('Error: Images Only!');
  }
}

// @route   POST /upload
// @desc    Upload file to server
router.post('/upload', (req, res) => {
  upload(req, res, (err) => {
    if (err) {
      res.status(400).json({ message: err });
    } else {
      if (req.file === undefined) {
        res.status(400).json({ message: 'No file selected!' });
      } else {
        res.status(200).json({
          message: 'File uploaded!',
          file: `uploads/${req.file.filename}`
        });
      }
    }
  });
});

module.exports = router;

```
### 3. Συμπεριλάβετε το Upload API στο Main φάκελο
```javascript
// server.js
const express = require('express');
const path = require('path');

const app = express();

// Bodyparser Middleware
app.use(express.json());
app.use(express.urlencoded({ extended: true }));

// Set static folder for serving files
app.use('/uploads', express.static(path.join(__dirname, 'uploads')));

// Upload route
const uploadRoute = require('./upload');
app.use('/api', uploadRoute);

const PORT = process.env.PORT || 5000;
app.listen(PORT, () => console.log(`Server started on port ${PORT}`));

```
## Λήψη αρχείων

### 1. Δημιουργία ενός API για λήψη αρχείων
```javascript
// download.js
const express = require('express');
const path = require('path');
const router = express.Router();

// @route   GET /download/:filename
// @desc    Download file from server
router.get('/download/:filename', (req, res) => {
  const file = path.join(__dirname, 'uploads', req.params.filename);
  res.download(file, (err) => {
    if (err) {
      res.status(400).json({ message: 'File not found' });
    }
  });
});

module.exports = router;

```
### 2. Συμπεριλάβετε το API λήψης στο κύριο αρχείο

```javascript
// server.js (continuing from before)
const downloadRoute = require('./download');
app.use('/api', downloadRoute);


```
## Περίληψη
Αυτό το παράδειγμα χρησιμοποιεί το multer για τη μεταφόρτωση αρχείων και το express για τη λήψη αρχείων. Τα αρχεία αποθηκεύονται τοπικά στον κατάλογο uploads και εξυπηρετούνται στατικά.

- Κατά τη διάρκεια της μεταφόρτωσης αρχείων, ο διακομιστής επικυρώνει:
  - Το αρχείο πρέπει να είναι εικόνα (jpeg, jpg, png, gif).
  - Το μέγεθος του αρχείου δεν πρέπει να υπερβαίνει το 1MB.
- Κατά τη λήψη αρχείων, ο διακομιστής επιτρέπει τη λήψη αρχείων με το όνομά τους, εφόσον υπάρχουν στον διακομιστή.
