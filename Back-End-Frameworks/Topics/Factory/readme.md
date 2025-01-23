# Μοντέλο σχεδίασης Factory 

Το πρότυπο σχεδίασης _Factory_ είναι ένα πρότυπο δημιουργίας. Ένα «εργοστάσιο» είναι μια υπερκλάση της οποίας οι υποκλάσεις μπορούν να επηρεάσουν ποιες παράμετροι χρησιμοποιούνται για τη δημιουργία ενός αντικειμένου. Η υπερκλάση factory κάνει δύο πράγματα:

- δημιουργεί αντικείμενα χρησιμοποιώντας μια  **hidden** μέθοδο υπερκλάσης
- αναφέρεται στο δημιουργημένο αντικείμενο μέσω μιας  **common** διεπαφής

Ο στόχος είναι η μείωση του κώδικα και η ελαχιστοποίηση του τεχνικού χρέους. Κυρίως, θα πρέπει να μειωθεί η δημιουργία νέων αντικειμένων με τη χρήση της λέξης κλειδί `new`, για παράδειγμα:

```js
const bear = new Bear();
const parrot = new Parrot();
const goldfish = new Goldfish();
// etc.
```

---

## Περίπτωση χρήσης
Το πρότυπο σχεδίασης εργοστασίων αντιμετωπίζει προβλήματα που προκύπτουν όταν η δημιουργία αντικειμένων γίνεται πολύπλοκη ή εξαρτάται από δυναμικές συνθήκες. Αυτό το πρότυπο διαχωρίζει τη λογική της δημιουργίας αντικειμένων από τη χρήση τους, επιτρέποντας στο σύστημα να είναι πιο ευέλικτο και πιο εύκολο στη συντήρηση.

Τρία συστατικά στοιχεία στο πρότυπο Factory:

1. **Product**: Το αντικείμενο που δημιουργείται, το οποίο έχει μια κοινή διεπαφή, κρυμμένη από τον πελάτη.
2. **Factory**: Η κλάση που περιέχει τη μέθοδο για τη δημιουργία αντικειμένων, συνήθως κρυμμένη από τον πελάτη.
3. **Client**: Η κλάση που χρησιμοποιεί το εργοστάσιο για τη δημιουργία αντικειμένων. Αυτό είναι το μέρος που χρησιμοποιεί το εργοστάσιο.

---

## Παράδειγμα

### Cat Υπερκλάση  ("Product" Component)

```js
// Superclass for a common interface
class Cat {
  constructor(name, age, color) {
    this.name = name;
    this.age = age;
    this.color = color;
  }
  introduce() {
    console.log(
      `My cat's name is ${this.name}, he is ${this.age} years old, and his fur color is ${this.color}.`
    );
  }
}
```

### Factory κλάση ("Factory" Component)

```js
class CatFactory {
  createCat(name, age, color) {
    // Factories should always contain at least a 'create()' method.
    return new Cat(name, age, color);
  }
}
```

Το εργοστάσιο μπορεί επίσης να υλοποιηθεί ως συνάρτηση, αποδίδοντας το ίδιο αποτέλεσμα.

```js
function CatFactory(name, age, color) {
  return new Cat(name, age, color);
}
```

### Χρήση του Factory ("Client" Component)

```js
const factory = new CatFactory();
const myCat = factory.createCat("Tom", 3, "gray");
const myOtherCat = factory.createCat("Max", 2, "white");
myCat.introduce(); // My cat's name is Tom, he is 3 years old, and his fur color is gray.
myOtherCat.introduce(); // My cat's name is Max, he is 2 years old, and his fur color is white.
```

---

## Πιο σύνθετο παράδειγμα

Στο προηγούμενο παράδειγμα, ασχοληθήκαμε μόνο με γάτες. Τώρα, ας τροποποιήσουμε τα πράγματα για να φιλοξενήσουμε τόσο γάτες όσο και σκύλους.

### Product

```js
// Superclass for a common interface
class Animal {
  constructor(name, age, color, type) {
    this.name = name;
    this.age = age;
    this.color = color;
    this.type = type; // Adding the type of animal
  }
  introduce() {
    console.log(
      `My pet's name is ${this.name}, he is ${this.age} years old, and he is ${this.color} in color.`
    );
  }
  logActivity() {
    console.log(
      `Animal type: ${this.type}, activity: ${this.currentActivity()}`
    );
  }
  currentActivity() {
    return "Normal activity";
  }
}
```

### Υποκλάσεις

Σε σύγκριση με το προηγούμενο παράδειγμα, τώρα προσθέτουμε υποκλάσεις στην κλάση _Animal_. Αυτό μας επιτρέπει να προσθέτουμε μοναδικές ιδιότητες ανάλογα με τις ανάγκες.

```js
class Cat extends Animal {
  constructor(name, age, color) {
    super(name, age, color, "Cat"); // Setting the type immediately since this class corresponds to that animal
  }
  currentActivity() {
    return "Playing with a toy mouse";
  }
}

class Dog extends Animal {
  constructor(name, age, color) {
    super(name, age, color, "Dog");
  }
  currentActivity() {
    return "Running around outside";
  }
}
```

### Factory

Εδώ, προσθέτω επίσης το _'type'_, το οποίο κάνει διάκριση μεταξύ των δύο ζώων που δημιουργούνται.

```js
class AnimalFactory {
  createAnimal(type, name, age, color) {
    if (type === "Cat") {
      return new Cat(name, age, color);
    } else if (type === "Dog") {
      return new Dog(name, age, color);
    } else {
      throw new Error("Invalid animal type"); // Our factory currently does not support other animals.
    }
  }
}
```

### Client

```js
const factory = new AnimalFactory();
const myCat = factory.createAnimal("Cat", "Tom", 3, "gray");
const myDog = factory.createAnimal("Dog", "Rex", 5, "brown");

myCat.introduce();
myDog.introduce();

myCat.logActivity(); // Animal type: Cat, activity: Playing with a toy mouse
myDog.logActivity(); // Animal type: Dog, activity: Running around outside
```

---

## Άσκηση

**Περιγραφή**: Ο κώδικας πρέπει να αποθηκεύει τους υπαλλήλους της εταιρείας σε μια βάση δεδομένων. Η βάση δεδομένων περιγράφει τους υπαλλήλους με τρεις ιδιότητες: όνομα, θέση εργασίας και επίπεδο διοίκησης.

**Εργασίες**: Δημιουργήστε ένα προϊόν, ένα εργοστάσιο για την παραγωγή του προϊόντος και δημιουργήστε αντικείμενα μέσω του εργοστασίου σε μια "βάση δεδομένων" (η βάση δεδομένων εδώ είναι ένας άδειος πίνακας `[]`).

**Αναμενόμενο αποτέλεσμα**: Το αποτέλεσμα του `console.log(database)` θα πρέπει να είναι:

```json
[
  { "name": "John", "job": "Team lead", "level": "Senior" },
  { "name": "Mary", "job": "Developer", "level": "Junior" },
  { "name": "Juku", "job": "Tester", "level": "Intern" }
]
```

---

**Πηγές**:

- [Oodesign - factory pattern](https://www.oodesign.com/factory-pattern)
- [Refactoring Guru - factory method](https://refactoring.guru/design-patterns/factory-method)

**Author: Taavi Ansper**

## Μοντέλο σχεδίασης εργοστασίων με λειτουργική προσέγγιση

Το πρότυπο σχεδίασης `Factory` μπορεί επίσης να χρησιμοποιηθεί αποτελεσματικά χρησιμοποιώντας μια λειτουργική προσέγγιση. Ο απλούστερος τρόπος είναι η δημιουργία μιας συνάρτησης που επιστρέφει ένα νέο αντικείμενο. Για παράδειγμα:
```js
function createCat(name, age, color) {
  return {
    name,
    age,
    color,
    introduce() {
      console.log(
        `My cat's name is ${this.name}, he is ${this.age} years old, and his fur color is ${this.color}.`
      );
    },
  };
}

const myCat = createCat("Tom", 3, "gray");
myCat.introduce(); // My cat's name is Tom, he is 3 years old, and his fur color is gray.
```
