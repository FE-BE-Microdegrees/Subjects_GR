# Ενσωματωμένες ενότητες

- [Ενσωματωμένες ενότητες](#Ενσωματωμένες-ενότητες)
  - [Μαθησιακά αποτελέσματα](#Μαθησιακά-αποτελέσματα)
  - [Εισαγωγή ενσωματωμένων ενοτήτων](#Εισαγωγή-ενσωματωμένων-ενοτήτων)
  - [Χρησιμοποιώντας Ενσωματωμένες Ενότητες](#Χρησιμοποιώντας-Ενσωματωμένες-Ενότητες)
  - [Κατάλογος ενσωματωμένων ενοτήτων](#Κατάλογος-ενσωματωμένων-ενοτήτων)
  - [`fs` Module](#fs-module)
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

## Using Built-In Modules

Built-in modules are used in the same way as user-created modules.

For instance, to read the contents of a file, you can use the `fs` module:

```javascript
const fs = require('fs');

fs.readFile('file.txt', 'utf8', (err, data) => {
  if (err) throw err;
  console.log(data);
});
```

In this example, the contents of the file `file.txt` are read and displayed in the console.

## List of Built-In Modules

Here are some built-in modules available for use:

- `fs` - File System module
- `path` - Path module
- `os` - Operating System module
- `util` - Utility module
- `events` - Events module
- `http` - HTTP module
- `crypto` - Cryptography module
- `zlib` - Compression module
- `stream` - Stream module
- ...

For a complete list of built-in modules, refer to the [official Node.js documentation](https://nodejs.org/dist/latest-v19.x/docs/api/).

## `fs` Module

The `fs` module is a built-in Node.js module that allows working with the file system. It supports reading, writing, modifying, and deleting files.

### Reading a File

To read a file, use the  `fs.readFile` method. For example:

```javascript
const fs = require('fs');

fs.readFile('file.txt', 'utf8', (err, data) => {
  if (err) throw err;
  console.log(data);
});
```

You can also use the synchronous method `fs.readFileSync`:

```javascript
const fs = require('fs');

const data = fs.readFileSync('file.txt', 'utf8');
console.log(data);
```

> Note: Use synchronous methods only when you're certain it won't block other processes, as they may slow down the application.
> 
### Writing a File

To write to a file, use the `fs.writeFile` method. For example:

```javascript
const fs = require('fs');

fs.writeFile('file.txt', 'Hello, World!', (err) => {
  if (err) throw err;
  console.log('File has been written!');
});
```

You can also use the synchronous method `fs.writeFileSync` 

```javascript
const fs = require('fs');

fs.writeFileSync('file.txt', 'Hello, World!');
console.log('File has been written!');
```

### Deleting a File

To delete a file, use the  `fs.unlink` method. For example:

```javascript
const fs = require('fs');

fs.unlink('file.txt', (err) => {
  if (err) throw err;
  console.log('File has been deleted!');
});
```

You can also use the synchronous method `fs.unlinkSync`:

```javascript
const fs = require('fs');

fs.unlinkSync('file.txt');
console.log('File has been deleted!');
```

## `path` Module

The `path` module is a built-in Node.js module that helps with file paths and names. It allows creating, modifying, and analyzing paths to files and directories.

### Creating a Path

To create a path, use the `path.join` method. For example:

```javascript
const path = require('path');

const filePath = path.join(__dirname, 'file.txt');
console.log(filePath);
```

This example generates a path to the file `file.txt` using the `__dirname` variable, which points to the current directory.

## `os` Module

The `os` module is a built-in Node.js module that provides information about the operating system. It supports retrieving data such as the OS version, architecture, CPU details, username, and home directory.

### Operating System Information

To retrieve OS information, use methods provided by the os module. For example:

```javascript
const os = require('os');

console.log(os.platform()); // 'win32'
console.log(os.arch()); // 'x64'
console.log(os.cpus()); // [{ model: 'Intel(R) Core(TM) i7-7700HQ CPU @ 2.80GHz', speed: 2808, times: { user: 0, nice: 0, sys: 0, idle: 0, irq: 0 } }]

// ...
```
