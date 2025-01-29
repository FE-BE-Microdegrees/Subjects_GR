# Ενότητες Third-Party 

Για μια εισαγωγή στα modules της JavaScript, ανατρέξτε στο [Modules](../Modules/README.md).

Εκτός από τα modules που δημιουργούνται από τον χρήστη και τα ενσωματωμένα modules, το Node.js επιτρέπει επίσης τη χρήση modules τρίτων κατασκευαστών. Αυτές οι ενότητες δημιουργούνται από άλλους προγραμματιστές και είναι διαθέσιμες μέσω του μητρώου *[Node Package Manager (NPM)](https://www.npmjs.com/)*.

- [Ενότητες Third-Party ](#Ενότητες-Third---Party )
  - [Μαθησιακά αποτελέσματα](#Μαθησιακά-αποτελέσματα)
  - [NPM](#npm)
  - [package.json](#packagejson)
  - [Εγκατάσταση ενοτήτων Third-Party](#Εγκατάσταση-ενοτήτων-Third---Party)
  - [Ο φάκελος `node_modules`](#Ο-φάκελος-`node_modules`)
  - [Επαναφορά του φακέλου `node_modules`](#Επαναφορά-του-φακέλου-node_modules-folder)
  - [Χρήση ενοτήτων Third-Party](#Χρήση-ενοτήτων-Third-Party])
  - [Αφαίρεση ενοτήτων Third-Party](#Αφαίρεση-ενοτήτων-Third-Party)
  - [Εγκατάσταση και χρήση ενότητας Third-Party](#Εγκατάσταση-και-χρήση-ενότητας-Third-Party)
  - [Κατάλογος χρήσιμων ενοτήτων Third-Party](#Κατάλογος-χρήσιμων-ενοτήτων-Third-Party)
  - [Ασκήσεις](#Ασκήσεις)
    - [Ασκήσεις 1](#Ασκήσεις-1)
    - [Ασκήσεις 2](#Ασκήσεις-2)
    - [Ασκήσεις 3](#Ασκήσεις-3)
    - [Ασκήσεις 4](#Ασκήσεις-4)

## Μαθησιακά αποτελέσματα

Μετά την ολοκλήρωση αυτού του θέματος, θα:

- Κατανοήσετε τι είναι οι ενότητες τρίτων κατασκευαστών.
- Να είστε σε θέση να δημιουργήσετε ένα αρχείο `package.json`.
- Να γνωρίζετε πώς να εγκαθιστάτε ενότητες τρίτων κατασκευαστών.
- Να γνωρίζετε πώς να χρησιμοποιείτε ενότητες τρίτων κατασκευαστών.

## NPM

Το NPM, ή Node Package Manager, είναι το σύστημα διαχείρισης πακέτων του Node.js. Επιτρέπει στους προγραμματιστές να κατεβάζουν και να χρησιμοποιούν ενότητες που έχουν δημιουργηθεί από άλλους. Το NPM συνοδεύει το Node.js και η πρόσβαση σε αυτό γίνεται μέσω της γραμμής εντολών. Οι ενότητες τρίτων αποθηκεύονται στο [NPM registry](https://www.npmjs.com/), το οποίο περιέχει χιλιάδες ενότητες σχεδιασμένες για την επίλυση διαφόρων προβλημάτων, όπως:

- [Express](https://www.npmjs.com/package/express) - Για τη δημιουργία διαδικτυακών εφαρμογών.
- [MySQL](https://www.npmjs.com/package/mysql) - Για την αλληλεπίδραση με βάσεις δεδομένων MySQL.
- [Axios](https://www.npmjs.com/package/axios) - Για την πραγματοποίηση αιτημάτων HTTP.
- [prompt-sync](https://www.npmjs.com/package/prompt-sync) - Για την αποδοχή εισόδου χρήστη στο Node.js.

## package.json

Για τη χρήση ενοτήτων τρίτων κατασκευαστών, πρέπει να δημιουργηθεί ένα αρχείο `package.json` στον ριζικό κατάλογο του έργου. Αυτό το αρχείο περιέχει τη διαμόρφωση και τις εξαρτήσεις του έργου. Οι εξαρτήσεις είναι οι ενότητες που χρησιμοποιούνται από το έργο. Για παράδειγμα, αν το έργο σας χρησιμοποιεί το module `prompt-sync`, πρέπει να το προσθέσετε ως εξάρτηση στο αρχείο `package.json`.

Δημιουργήστε ένα αρχείο `package.json` χρησιμοποιώντας την ακόλουθη εντολή:

```bash
npm init -y
```

Αυτή η εντολή δημιουργεί ένα αρχείο `package.json` με προεπιλεγμένες τιμές:

```json
{
  "name": "project-name",
  "version": "1.0.0",
  "description": "Project description",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "Author name",
  "license": "MIT",
}
```

Μπορείτε να ρυθμίσετε λεπτομερώς το έργο σας χρησιμοποιώντας το npm init και ακολουθώντας τις οδηγίες.

## Εγκατάσταση ενοτήτων Third-Party

Όταν υπάρχει ένα αρχείο `package.json`, οι ενότητες τρίτων μπορούν να εγκατασταθούν χρησιμοποιώντας την ακόλουθη εντολή:

```bash
npm install <module-name>
```

Για παράδειγμα, για να εγκαταστήσετε την ενότητα `prompt-sync`:

```bash
npm install prompt-sync
```

Αυτή η εντολή εγκαθιστά την ενότητα `prompt-sync` στο ριζικό κατάλογο του έργου και την προσθέτει στη λίστα εξαρτήσεων στο αρχείο `package.json` .

```json
{
  "name": "project-name",
  "version": "1.0.0",
  "description": "Project description",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "Author name",
  "license": "MIT",
  "dependencies": {
    "prompt-sync": "^4.2.0"
  }
}
```


## Ο φάκελος `node_modules`

Οι εγκατεστημένες ενότητες αποθηκεύονται στο φάκελο `node_modules`. στο ριζικό κατάλογο του έργου. Αυτός ο φάκελος περιλαμβάνει όλες τις εξαρτήσεις του έργου και τις εξαρτήσεις τους. Μπορεί να γίνει μεγάλος και δεν συνιστάται για έλεγχο εκδόσεων (π.χ. Git). Αντ' αυτού, προσθέστε τον στον φάκελο `.gitignore`.

 `.gitignore` example:

```plaintext
node_modules/
```


## Επαναφορά του φακέλου `node_modules`

Επαναφορά του φακέλου node_modules Ο φάκελος `node_modules` δεν περιλαμβάνεται στον έλεγχο έκδοσης, άλλοι προγραμματιστές μπορούν να τον επαναδημιουργήσουν χρησιμοποιώντας την ακόλουθη εντολή στον ριζικό κατάλογο του έργου (όπου βρίσκεται το αρχείο `package.json`):

```bash
npm install
```

Αυτή η εντολή δημιουργεί το `node_modules` παλαιότερα με βάση τις εξαρτήσεις που αναφέρονται στο `package.json`.

## Χρήση ενοτήτων Third-Party

Μετά την εγκατάσταση μιας ενότητας, μπορεί να χρησιμοποιηθεί στον κώδικα όπως οποιαδήποτε άλλη ενότητα. Για παράδειγμα, χρησιμοποιώντας την ενότητα `prompt-sync`:

```javascript
const prompt = require('prompt-sync'); // Import the module

const prompts = prompt(); // Initialize the module

const age = prompts('Enter your age: '); // Get user input

console.log(age); // Output the input

```

Σε αυτό το παράδειγμα, η ενότητα `prompt-sync` χρησιμοποιείται για να ζητάει από τον χρήστη την ηλικία του και να την εμφανίζει στην κονσόλα.

## Αφαίρεση ενοτήτων Third-Party

Για να αφαιρέσετε μια εγκατεστημένη μονάδα, χρησιμοποιήστε την ακόλουθη εντολή:

```bash
npm uninstall <module-name>
```

Για παράδειγμα, για να απεγκαταστήσετε το `prompt-sync` :

```bash
npm uninstall prompt-sync
```

Αυτό αφαιρεί την ενότητα από το φάκελο `prompt-sync` και τη λίστα εξαρτήσεων στο `package.json`.

## Εγκατάσταση και χρήση ενότητας Third-Party

![Εγκατάσταση και χρήση ενότητας Third-Party](thirdPartyModules.gif)

## Κατάλογος χρήσιμων ενοτήτων Third-Party

Ακολουθούν ορισμένες χρήσιμες ενότητες third-party:

- [Nodemon](https://www.npmjs.com/package/nodemon) - Αυτόματη επανεκκίνηση των εφαρμογών Node.js.
- [prompt-sync](https://www.npmjs.com/package/prompt-sync) - Για την αποδοχή της εισόδου του χρήστη.
- [colors](https://www.npmjs.com/package/colors) - Για έγχρωμο κείμενο κονσόλας.
- [nodemailer](https://www.npmjs.com/package/nodemailer) - Για την αποστολή μηνυμάτων ηλεκτρονικού ταχυδρομείου.
- [cron](https://www.npmjs.com/package/cron) - Για τον προγραμματισμό εργασιών.

## Ασκήσεις

### Άσκηση 1

Δημιουργήστε ένα πρόγραμμα που ζητά από τον χρήστη ένα όνομα χρήστη και έναν κωδικό πρόσβασης. Εάν το όνομα χρήστη είναι admin και ο κωδικός πρόσβασης είναι 1234, εμφανίστε το μήνυμα Welcome!. Διαφορετικά, εμφανίστε Invalid username or password!.

<details> <summary>Hint 1</summary>
Create a package.json file using npm init -y.

</details> <details> <summary>Hint 2</summary>
Use the prompt-sync module for user input. Install it with npm install prompt-sync.

</details> <details> <summary>Solution</summary>
  
  ```javascript
const prompts = require('prompt-sync');

const prompt = prompts();

const username = prompt('Palun sisesta oma kasutajanimi: ');
const password = prompt('Palun sisesta oma parool: ');

if (username === 'admin' && password === '1234') {
  console.log('Tere tulemast!');
} else {
  console.log('Vale kasutajanimi või parool!');
}

```

</details>

### Άσκηση 2

Βελτιώστε το πρόγραμμα ώστε να επιτρέπει στον χρήστη να εισάγει εκ νέου το όνομα χρήστη και τον κωδικό πρόσβασής του σε περίπτωση λανθασμένων στοιχείων.

<details> <summary>Hint</summary>
Use a loop (e.g., while) to repeat the input prompt until the correct credentials are provided.

</details>

### Άσκηση 3

Τροποποιήστε το πρόγραμμα ώστε να περιορίσετε τον αριθμό των λανθασμένων προσπαθειών σε τρεις. Μετά από τρεις λανθασμένες προσπάθειες, τερματίστε το πρόγραμμα με το μήνυμα Too many invalid attempts!.

### Άσκηση 4

Προσθέστε χρώμα στις εξόδους του προγράμματος χρησιμοποιώντας την ενότητα colors. Για παράδειγμα, εμφανίστε το Welcome! με πράσινο χρώμα και το Invalid username or password! με κόκκινο χρώμα.

<details> <summary>Hint 1</summary>
Install the colors module using npm install colors.

</details> <details> <summary>Hint 2</summary>
Use methods like colors.green and colors.red for colored output:

</details>
