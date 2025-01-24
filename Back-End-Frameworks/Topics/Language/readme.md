# Επιλογή γλώσσας στο Express API

Για να υλοποιήσετε την επιλογή γλώσσας σε ένα API Express, μπορείτε να χρησιμοποιήσετε πλαίσια διεθνοποίησης (i18n) όπως τα `i18next`, `i18next-express-middleware` και `i18next-http-backend`. Αυτά τα εργαλεία επιτρέπουν τη διαχείριση πολύγλωσσων μεταφράσεων και τον καθορισμό της γλώσσας με βάση τις προτιμήσεις του πελάτη.

## Εγκαταστήστε τα απαιτούμενα πακέτα

Εγκαταστήστε τα `i18next`, `i18next-express-middleware` και `i18next-http-backend`:

```bash
npm install i18next i18next-express-middleware i18next-http-backend
```

## Διαμόρφωση του i18next

Δημιουργήστε ένα αρχείο `i18next.js` που περιέχει τις ρυθμίσεις του i18next:

```javascript
// i18next.js
const i18n = require('i18next');
const Backend = require('i18next-http-backend');
const middleware = require('i18next-express-middleware');

i18n
  .use(Backend)
  .use(middleware.LanguageDetector)
  .init({
    fallbackLng: 'en', // default language
    preload: ['en', 'et'], // preload languages
    backend: {
      loadPath: __dirname + '/locales/{{lng}}/{{ns}}.json'
    }
  });

module.exports = i18n;

```

## Δημιουργία αρχείων μετάφρασης

Δημιουργήστε ένα φάκελο `locales` και υποφακέλους για κάθε γλώσσα, όπως `en` και `et`. Μέσα σε κάθε φάκελο, δημιουργήστε αρχεία μετάφρασης όπως το `translation.json`:

### `locales/en/translation.json`

```json
{
  "welcome": "Welcome",
  "message": "This is an internationalized message."
}
```

### `locales/et/translation.json`

```json
{
  "welcome": "Tere tulemast",
  "message": "See on rahvusvaheline sõnum."
}
```

## Προσθήκη i18next Middleware στο Express API

Ρύθμιση του API Express για χρήση του i18next:


```javascript
// server.js
const express = require('express');
const i18next = require('./i18next');
const middleware = require('i18next-express-middleware');

const app = express();

app.use(middleware.handle(i18next));

// Bodyparser Middleware
app.use(express.json());
app.use(express.urlencoded({ extended: true }));

// Example route with translation
app.get('/api', (req, res) => {
  const welcomeMessage = req.t('welcome');
  const message = req.t('message');
  res.json({ welcomeMessage, message });
});

const PORT = process.env.PORT || 5000;
app.listen(PORT, () => console.log(`Server started on port ${PORT}`));

```

## Χρήση επιλογής γλώσσας στο πρόγραμμα-πελάτη

Μπορείτε να ορίσετε τη γλώσσα στην πλευρά του πελάτη χρησιμοποιώντας την επικεφαλίδα HTTP `Accept-Language` ή μια παράμετρο URL.

### Παράδειγμα: HTTP Header

Συμπεριλάβετε την επικεφαλίδα `Accept-Language` στην αίτηση API:

```sh
curl -H "Accept-Language: et" http://localhost:5000/api
```

### Παράδειγμα: Χρήση παραμέτρου URL

Για να χρησιμοποιήσετε μια παράμετρο URL για την επιλογή γλώσσας, ρυθμίστε το ενδιάμεσο λογισμικό i18next ώστε να ανιχνεύει τη γλώσσα από τη συμβολοσειρά ερωτήματος:

```javascript
// i18next.js (add lookupQuery)
i18n
  .use(Backend)
  .use(middleware.LanguageDetector)
  .init({
    fallbackLng: 'en',
    preload: ['en', 'et'],
    backend: {
      loadPath: __dirname + '/locales/{{lng}}/{{ns}}.json'
    },
    detection: {
      order: ['querystring', 'cookie', 'header'],
      caches: ['cookie'],
      lookupQuerystring: 'lng'
    }
  });

module.exports = i18n;

```

Τώρα, ορίστε τη γλώσσα χρησιμοποιώντας την παράμετρο URL:

```sh
curl http://localhost:5000/api?lng=et
```

## Περίληψη

Σε αυτό το παράδειγμα, χρησιμοποιήσαμε το i18next και το i18next-express-middleware για να προσθέσουμε υποστήριξη διεθνοποίησης σε ένα API Express. Διαμορφώσαμε την επιλογή γλώσσας χρησιμοποιώντας την επικεφαλίδα Accept-Language και τις παραμέτρους URL. Αυτό επιτρέπει την παροχή πολύγλωσσων απαντήσεων με βάση τις προτιμήσεις του χρήστη.

