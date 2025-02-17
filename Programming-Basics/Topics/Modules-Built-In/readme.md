# Ενσωματωμένες ενότητες

- [Ενσωματωμένες ενότητες](#Ενσωματωμένες-ενότητες)
  - [Μαθησιακά αποτελέσματα](#Μαθησιακά-αποτελέσματα)
  - [Εισαγωγή ενσωματωμένων ενοτήτων](#Εισαγωγή-ενσωματωμένων-ενοτήτων)
  - [Χρησιμοποιώντας Ενσωματωμένες Ενότητες](#Χρησιμοποιώντας-Ενσωματωμένες-Ενότητες)
  - [Κατάλογος ενσωματωμένων ενοτήτων](#Κατάλογος-ενσωματωμένων-ενοτήτων)
  - [Ενότητα`fs`](#Ενότητα`fs`)
    - [Διαβάζοντας ένα αρχείο](#Διαβάζοντας-ένα-αρχείο)
    - [Γράφοντας ένα αρχείο](#Γράφοντας-ένα-αρχείο)
    - [Διαγραφή ενός αρχείου](#Διαγραφή-ενός-αρχείου)
  - [Ενότητα `path`](#Ενότητα-`path`)
    - [Δημιουργία Path](#Δημιουργία-Path)
  - [Ενότητα `os`](#Ενότητα-`os`)
    - [Πληροφορίες λειτουργικού συστήματος](#Πληροφορίες-λειτουργικού-συστήματος)
  - [Ασκήσεις](#Ασκήσεις)
    - [Άσκηση 1](#Άσκηση-1)
    - [Άσκηση 2](#Άσκηση-2)
    - [Άσκηση 3](#Άσκηση-3)

Για μια εισαγωγή στα modules της JavaScript, ανατρέξτε στο [Modules](../Modules/README.md).

Εκτός από τις ενότητες που δημιουργούνται από τον χρήστη, η JavaScript παρέχει επίσης ενσωματωμένες ενότητες. Πρόκειται για ενότητες που περιλαμβάνονται στο Node.js από προεπιλογή και μπορούν να χρησιμοποιηθούν χωρίς να τις κατεβάσετε ή να τις εγκαταστήσετε.

## Μαθησιακά αποτελέσματα

Μετά την ολοκλήρωση αυτού του θέματος, θα:

- Καταλάβετε τι είναι οι ενσωματωμένες ενότητες στο Node.js.
- Να είστε σε θέση να εισάγετε ενσωματωμένες ενότητες.
- Να είστε σε θέση να χρησιμοποιείτε τα ενσωματωμένα modules στο Node.js.

## Εισαγωγή ενσωματωμένων ενοτήτων

Για να χρησιμοποιήσετε ενσωματωμένες ενότητες, πρέπει πρώτα να τις εισάγετε. Για παράδειγμα:

```javascript
const fs = require('fs');
```

Όπως φαίνεται, οι ενσωματωμένες ενότητες μπορούν να εισαχθούν με τον ίδιο τρόπο όπως οι ενότητες που δημιουργούνται από τον χρήστη, αλλά δεν απαιτούν συγκεκριμένη διαδρομή- αρκεί μόνο το όνομα της ενότητας.

## Χρησιμοποιώντας Ενσωματωμένες Ενότητες

Οι ενσωματωμένες ενότητες χρησιμοποιούνται με τον ίδιο τρόπο όπως και οι ενότητες που δημιουργούνται από τον χρήστη.

Για παράδειγμα, για να διαβάσετε τα περιεχόμενα ενός αρχείου, μπορείτε να χρησιμοποιήσετε την ενότητα `fs`:

```javascript
const fs = require('fs');

fs.readFile('file.txt', 'utf8', (err, data) => {
  if (err) throw err;
  console.log(data);
});
```

Σε αυτό το παράδειγμα, τα περιεχόμενα του αρχείου `file.txt` διαβάζονται και εμφανίζονται στην κονσόλα.

## Κατάλογος ενσωματωμένων ενοτήτων

Ακολουθούν ορισμένες ενσωματωμένες ενότητες που είναι διαθέσιμες για χρήση:

- `fs` - Ενότητα File System
- `path` - Ενότητα Path 
- `os` -  Ενότητα Operating System
- `util` - Ενότητα Utility 
- `events` -   Ενότητα Events 
- `http` -  Ενότητα HTTP 
- `crypto` -  Ενότητα Cryptography 
- `zlib` -   Ενότητα Compression 
- `stream` -  Ενότητα Stream 
- ...

Για έναν πλήρη κατάλογο των ενσωματωμένων ενοτήτων, ανατρέξτε στην [επίσημη τεκμηρίωση του Node.js](https://nodejs.org/dist/latest-v19.x/docs/api/).

## Ενότητα`fs`

Η ενότητα `fs` είναι μια ενσωματωμένη ενότητα του Node.js που επιτρέπει την εργασία με το σύστημα αρχείων. Υποστηρίζει την ανάγνωση, εγγραφή, τροποποίηση και διαγραφή αρχείων.

### Διαβάζοντας ένα αρχείο

Για να διαβάσετε ένα αρχείο, χρησιμοποιήστε τη μέθοδο `fs.readFile`. Για παράδειγμα:

```javascript
const fs = require('fs');

fs.readFile('file.txt', 'utf8', (err, data) => {
  if (err) throw err;
  console.log(data);
});
```

Μπορείτε επίσης να χρησιμοποιήσετε τη σύγχρονη μέθοδο `fs.readFileSync`:

```javascript
const fs = require('fs');

const data = fs.readFileSync('file.txt', 'utf8');
console.log(data);
```

> Σημείωση: Χρησιμοποιήστε σύγχρονες μεθόδους μόνο όταν είστε σίγουροι ότι δεν θα μπλοκάρουν άλλες διεργασίες, καθώς μπορεί να επιβραδύνουν την εφαρμογή.


### Γράφοντας ένα αρχείο

Για να γράψετε σε ένα αρχείο, χρησιμοποιήστε τη μέθοδο `fs.writeFile`. Για παράδειγμα:

```javascript
const fs = require('fs');

fs.writeFile('file.txt', 'Hello, World!', (err) => {
  if (err) throw err;
  console.log('File has been written!');
});
```

Μπορείτε επίσης να χρησιμοποιήσετε τη σύγχρονη μέθοδο `fs.writeFileSync` 

```javascript
const fs = require('fs');

fs.writeFileSync('file.txt', 'Hello, World!');
console.log('File has been written!');
```

### Διαγραφή ενός αρχείου

Για να διαγράψετε ένα αρχείο, χρησιμοποιήστε τη μέθοδο `fs.unlink`. Για παράδειγμα:

```javascript
const fs = require('fs');

fs.unlink('file.txt', (err) => {
  if (err) throw err;
  console.log('File has been deleted!');
});
```

Μπορείτε επίσης να χρησιμοποιήσετε τη σύγχρονη μέθοδο `fs.unlinkSync`:

```javascript
const fs = require('fs');

fs.unlinkSync('file.txt');
console.log('File has been deleted!');
```

## Ενότητα `path`

Η ενότητα `path` είναι μια ενσωματωμένη ενότητα του Node.js που βοηθάει με τις διαδρομές και τα ονόματα αρχείων. Επιτρέπει τη δημιουργία, την τροποποίηση και την ανάλυση διαδρομών σε αρχεία και καταλόγους.

### Δημιουργία Path

Για να δημιουργήσετε μια διαδρομή, χρησιμοποιήστε τη μέθοδο `path.join`. Για παράδειγμα:

```javascript
const path = require('path');

const filePath = path.join(__dirname, 'file.txt');
console.log(filePath);
```

Αυτό το παράδειγμα δημιουργεί μια διαδρομή προς το αρχείο `file.txt` χρησιμοποιώντας τη μεταβλητή `__dirname`, η οποία δείχνει στον τρέχοντα κατάλογο.

## Ενότητα `os`

Η ενότητα `os` είναι μια ενσωματωμένη ενότητα του Node.js που παρέχει πληροφορίες σχετικά με το λειτουργικό σύστημα. Υποστηρίζει την ανάκτηση δεδομένων όπως η έκδοση του λειτουργικού συστήματος, η αρχιτεκτονική, οι λεπτομέρειες της CPU, το όνομα χρήστη και ο κεντρικός κατάλογος.

###Πληροφορίες λειτουργικού συστήματος

Για να ανακτήσετε πληροφορίες για το λειτουργικό σύστημα, χρησιμοποιήστε τις μεθόδους που παρέχονται από την ενότητα os. Για παράδειγμα:

```javascript
const os = require('os');

console.log(os.platform()); // 'win32'
console.log(os.arch()); // 'x64'
console.log(os.cpus()); // [{ model: 'Intel(R) Core(TM) i7-7700HQ CPU @ 2.80GHz', speed: 2808, times: { user: 0, nice: 0, sys: 0, idle: 0, irq: 0 } }]

// ...
```
