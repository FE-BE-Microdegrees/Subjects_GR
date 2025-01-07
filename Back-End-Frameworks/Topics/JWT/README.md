# JWT (_JSON Web Token_)

Σε αυτή την ενότητα, θα συζητήσουμε το JWT (_JSON Web Token_), ένα ανοιχτό πρότυπο που χρησιμοποιείται για την ασφαλή μετάδοση δεδομένων μεταξύ των μερών σε μορφή JSON.

![JWT](JWT.webp)

Image source: DALL-E by OpenAI

## Μαθησιακά αποτελέσματα

Στο τέλος αυτής της ενότητας, οι μαθητές θα πρέπει να είναι σε θέση να:

- Εξηγήστε τι είναι το JWT και πώς λειτουργεί.
- Περιγράψτε τη δομή του JWT και τα στοιχεία του.
- Δημιουργία και επικύρωση JWT.
- Χρήση JWT σε διαδικασίες ελέγχου ταυτότητας και εξουσιοδότησης.

## JWT

Το JWT (_JSON Web Token_) είναι ένα ανοικτό πρότυπο (RFC 7519) που χρησιμοποιείται για την ασφαλή μετάδοση δεδομένων μεταξύ μερών σε μορφή JSON. Είναι ιδιαίτερα χρήσιμο για τον έλεγχο ταυτότητας και την ανταλλαγή πληροφοριών, επιτρέποντας την αξιόπιστη και αποτελεσματική μεταφορά πληροφοριών. Τα JWT είναι συμπαγή και εύκολα στη χρήση σε διάφορα σενάρια, όπως η αυθεντικοποίηση και η εξουσιοδότηση σε διαδικτυακές εφαρμογές.

### Στοιχεία JWT

Ένα JWT αποτελείται από τρία μέρη, τα οποία χωρίζονται με τελείες (.):

- **Επικεφαλίδα:** Περιέχει πληροφορίες σχετικά με τον τύπο του διακριτικού και τον αλγόριθμο υπογραφής που χρησιμοποιείται (π.χ. HMAC SHA256 ή RSA).

```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

- **Payload:** Περιέχει ισχυρισμούς, οι οποίοι είναι οι κωδικοποιημένες πληροφορίες στο JWT. Οι αξιώσεις μπορεί να είναι τυποποιημένες, δημόσιες ή ιδιωτικές.


```json
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true
}
```

- **Υπογραφή:** Δημιουργήθηκε για να διασφαλίσει την ακεραιότητα και την αυθεντικότητα του διακριτικού. Η υπογραφή δημιουργείται χρησιμοποιώντας ένα μυστικό κλειδί ή ένα ζεύγος δημόσιου/ιδιωτικού κλειδιού.

```bash
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret
)
```

### Δομή του JWT

TΗ πλήρης δομή του JWT μοιάζει ως εξής:

```bash
xxxxx.yyyyy.zzzzz
```

Όπου `xxxxx` είναι η επικεφαλίδα, `yyyyy` είναι το ωφέλιμο φορτίο και `zzzzz` είναι η υπογραφή, όλα κωδικοποιημένα σε base64-url.

## Πότε να χρησιμοποιήσετε το JWT;

- **Εξουσιοδότηση:** Αυτό είναι το πιο συνηθισμένο σενάριο για τη χρήση JWT. Μόλις συνδεθεί ένας χρήστης, κάθε επόμενη αίτηση περιέχει ένα JWT, επιτρέποντας στον χρήστη να έχει πρόσβαση στις διαδρομές, τις υπηρεσίες και τους πόρους που είναι εξουσιοδοτημένοι για το συγκεκριμένο token.
- **Ανταλλαγή πληροφοριών:** Τα JSON Web Tokens είναι ένας καλός τρόπος για την ασφαλή μετάδοση πληροφοριών μεταξύ των μερών. Δεδομένου ότι τα JWT μπορούν να υπογραφούν, για παράδειγμα, χρησιμοποιώντας ζεύγη δημόσιων/ιδιωτικών κλειδιών, μπορείτε να είστε σίγουροι ότι οι αποστολείς είναι αυτοί που λένε ότι είναι. Επιπλέον, επειδή η υπογραφή υπολογίζεται χρησιμοποιώντας την επικεφαλίδα και το ωφέλιμο φορτίο, μπορείτε επίσης να επαληθεύσετε ότι το περιεχόμενο δεν έχει τροποποιηθεί.

### Πλεονεκτήματα

- **Compactness:** Τα JWT είναι συμπαγή, πράγμα που σημαίνει ότι μπορούν να μεταδοθούν εύκολα μέσω διευθύνσεων URL, κεφαλίδων HTTP και δεδομένων POST.
- **Αυτόνομο:** Τα διακριτικά είναι αυτοτελή, καθώς περιέχουν όλες τις απαραίτητες πληροφορίες. Μπορείτε να επικυρώσετε το token χωρίς πρόσθετα δεδομένα, καθιστώντας το σύστημα πιο αποτελεσματικό και ευέλικτο.
- **Ασφάλεια:** Τα JWT διασφαλίζουν την ακεραιότητα των δεδομένων και επιτρέπουν τον έλεγχο ταυτότητας και την εξουσιοδότηση, κάτι που είναι χρήσιμο για τη δημιουργία ασφαλών συνδέσεων.

### Μειονεκτήματα

- **Διαρροή Token:** Τα JWT δεν μπορούν να ανακληθούν ή να ακυρωθούν μετά την έκδοσή τους. Εάν ένα JWT διαρρεύσει, μπορεί να είναι επικίνδυνο, καθώς μπορεί να παρέχει μη εξουσιοδοτημένη πρόσβαση, γεγονός που απαιτεί πρόσθετα μέτρα προστασίας.

## Δημιουργία και επικύρωση JWTs

### Δημιουργία JWTs

Η διαδικασία δημιουργίας ενός JWT περιλαμβάνει τη δημιουργία της επικεφαλίδας, του ωφέλιμου φορτίου και της υπογραφής και, στη συνέχεια, τον συνδυασμό τους.

#### Παράδειγμα σε Node.js

Για να δημιουργήσετε και να επικυρώσετε JWTs στο Node.js, μπορείτε να χρησιμοποιήσετε τη βιβλιοθήκη `jsonwebtoken`.

- **Εγκαταστήστε τη βιβλιοθήκη jsonwebtoken:**

```bash
npm install jsonwebtoken
```

- **Δημιουργία ενός JWT:**

```javascript
const jwt = require("jsonwebtoken");

const payload = {
  sub: "1234567890",
  name: "John Doe",
  admin: true,
};

const secret = "your-256-bit-secret";

const token = jwt.sign(payload, secret, { algorithm: "HS256" });
console.log(token);
```

### Επικύρωση JWTs

Επικύρωση JWTs

#### Παράδειγμα σε Node.js

1. **Επικύρωση ενός JWT:**

```javascript
const token =
  "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.D1lvcHfxDQn0EnyFCWm08FUBKm0tC3GtBCVm5qkaGTI";

jwt.verify(token, secret, (err, decoded) => {
  if (err) {
    console.log("Token is invalid or expired.");
  } else {
    console.log("Token is valid:", decoded);
  }
});
```

## Χρήση του JWT για έλεγχο ταυτότητας και εξουσιοδότηση

### Αυθεντικοποίηση

Τα JWT χρησιμοποιούνται συχνά για τον έλεγχο ταυτότητας χρηστών. Όταν ένας χρήστης συνδέεται, ο διακομιστής δημιουργεί ένα JWT που περιέχει την ταυτότητα του χρήστη και πιθανά δικαιώματα. Αυτό το JWT αποστέλλεται πίσω στον χρήστη και αποθηκεύεται στο πρόγραμμα περιήγησης ως cookie ή σε τοπικό αποθηκευτικό χώρο.


#### Παράδειγμα - 1

- **Σύνδεση χρήστη και δημιουργία JWT:**

```javascript
app.post("/login", (req, res) => {
  const { username, password } = req.body;
  // Check the username and password
  const user = users.find(
    (u) => u.username === username && u.password === password
  );
  if (user) {
    const token = jwt.sign({ sub: user.id, name: user.username }, secret, {
      expiresIn: "1h",
    });
    res.json({ token });
  } else {
    res.status(401).send("Invalid credentials");
  }
});
```

### Εξουσιοδότηση

Μόλις ένας χρήστης πιστοποιηθεί και αποκτήσει ένα JWT, ο διακομιστής μπορεί να χρησιμοποιήσει αυτό το token για να ελέγξει την ταυτότητα και τα δικαιώματα του χρήστη όταν ζητά προστατευμένους πόρους.


#### Example - 2

- **Using JWT for Authorization:**

```javascript
const authenticateJWT = (req, res, next) => {
  const token = req.header("Authorization");
  if (!token) return res.status(401).send("Access Denied");

  try {
    const verified = jwt.verify(token, secret);
    req.user = verified;
    next();
  } catch (error) {
    res.status(400).send("Invalid Token");
  }
};

app.get("/protected", authenticateJWT, (req, res) => {
  res.send("This is a protected route");
});
```

## Sources

- [JWT.io](https://jwt.io/)
- [RFC 7519: JSON Web Token (JWT)](https://tools.ietf.org/html/rfc7519)
- [jsonwebtoken Documentation](https://www.npmjs.com/package/jsonwebtoken)
- [Node.js Official Documentation](https://nodejs.org/en/docs/)

## Review Questions

- What is JWT and how does it work?
- Describe the structure of JWT and its components.
- How do you create and validate JWTs in Node.js using the `jsonwebtoken` library?
- How is JWT used in authentication and authorization processes?
- What are the advantages of using JWT?
