# Δοκιμές API Node με Supertest, Mocha και Chai: Εκτέλεση και δοκιμή της εφαρμογής

Οι δοκιμές API είναι απαραίτητες για να διασφαλιστεί η σωστή λειτουργία των τελικών σημείων της εφαρμογής σας. Σε αυτόν τον οδηγό, θα ρυθμίσουμε και θα δοκιμάσουμε ένα API Node.js χρησιμοποιώντας την Express με το Supertest, το Mocha και το Chai. Αρχικά θα διαχωρίσουμε τη λογική της εφαρμογής Express και την εκκίνηση του διακομιστή σε διαφορετικά αρχεία (`app.js` και `server.js`) για να απλοποιήσουμε τις δοκιμές. Στη συνέχεια, θα δημιουργήσουμε και θα εκτελέσουμε δοκιμές για την επικύρωση των τελικών σημείων του API.

---

## Μαθησιακοί στόχοι

Στο τέλος αυτού του σεμιναρίου, οι εκπαιδευόμενοι θα είναι σε θέση:

- Να ρυθμίζουν την εκκίνηση της εφαρμογής Express και του διακομιστή σε ξεχωριστά αρχεία.
- Να δοκιμάζουν τα τελικά σημεία API χρησιμοποιώντας το Supertest, το Mocha και το Chai.
- Να ελέγχουν την κάλυψη των δοκιμών χρησιμοποιώντας το εργαλείο `nyc`.

---

## Δομή του έργου

```plaintext
my-blog-api/
│
├── app.js          # Express application configuration
├── server.js       # Server startup
├── routes/
│   └── posts.js    # API endpoints
├── controllers/
│   └── postsController.js  # Controllers for endpoints
└── services/
    └── postsService.js     # Services for business logic
└── test/
    └── posts.test.js       # Tests for API endpoints
└── package.json    # Project configuration and dependencies
```

## Ρύθμιση API

### `app.js`

Ρυθμίστε την εφαρμογή Express και τις διαδρομές. Αυτό το αρχείο περιέχει τη λογική και τη διαμόρφωση της εφαρμογής χωρίς να εκκινήσετε το διακομιστή.

```javascript
const express = require('express');
const postsRouter = require('./routes/posts');

const app = express();

// Middleware for parsing JSON requests
app.use(express.json());

// Use routes for posts endpoints
app.use('/posts', postsRouter);

module.exports = app;

```

### `server.js`

Ξεκινήστε τον διακομιστή εισάγοντας την εφαρμογή από το αρχείο `app.js` και ακούγοντας σε μια καθορισμένη θύρα.

```javascript
const app = require('./app'); // Import the Express application
const PORT = process.env.PORT || 3000;

// Start the server
app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});
```

### `routes/posts.js`

Ορίστε τα τελικά σημεία API και συνδέστε τα με τους ελεγκτές στο αρχείο `postsController.js`.

```javascript
const express = require('express');
const router = express.Router();
const postsController = require('../controllers/postsController');

// Define endpoints and link to controllers
router.get('/', postsController.getAllPosts);
router.post('/', postsController.createPost);
router.put('/:id', postsController.updatePost);
router.delete('/:id', postsController.deletePost);

module.exports = router;
```

### `controllers/postsController.js`

Οι ελεγκτές χειρίζονται τα αιτήματα και τις απαντήσεις HTTP, αναθέτοντας τη λογική σε υπηρεσίες στο αρχείο `postsService.js`.

```javascript
const postsService = require('../services/postsService');

// Retrieve all posts
exports.getAllPosts = (req, res) => {
  const posts = postsService.getAllPosts();
  res.json(posts);
};

// Create a new post
exports.createPost = (req, res) => {
  const newPost = postsService.createPost(req.body);
  res.status(201).json(newPost);
};

// Update an existing post
exports.updatePost = (req, res) => {
  const updatedPost = postsService.updatePost(parseInt(req.params.id), req.body);
  if (updatedPost) {
    res.json(updatedPost);
  } else {
    res.status(404).send('Post not found');
  }
};

// Delete a post
exports.deletePost = (req, res) => {
  const deleted = postsService.deletePost(parseInt(req.params.id));
  if (deleted) {
    res.status(204).send();
  } else {
    res.status(404).send('Post not found');
  }
};

```

### `services/postsService.js`

Οι υπηρεσίες χειρίζονται την επιχειρησιακή λογική και τις λειτουργίες δεδομένων.

```javascript
let posts = [
  { id: 1, title: 'First Post', content: 'This is the first post' },
  { id: 2, title: 'Second Post', content: 'This is the second post' }
];

// Retrieve all posts
exports.getAllPosts = () => posts;

// Create a new post
exports.createPost = (postData) => {
  const newPost = {
    id: posts.length + 1,
    title: postData.title,
    content: postData.content
  };
  posts.push(newPost);
  return newPost;
};

// Update a post
exports.updatePost = (postId, postData) => {
  const postIndex = posts.findIndex(post => post.id === postId);
  if (postIndex !== -1) {
    posts[postIndex] = { id: postId, title: postData.title, content: postData.content };
    return posts[postIndex];
  }
  return null;
};

// Delete a post
exports.deletePost = (postId) => {
  const postIndex = posts.findIndex(post => post.id === postId);
  if (postIndex !== -1) {
    posts.splice(postIndex, 1);
    return true;
  }
  return false;
};

```

## Συγγραφή δοκιμών με Supertest, Mocha και Chai

Εγκαταστήστε τις απαιτούμενες εξαρτήσεις:

```bash
npm install --save-dev mocha chai@4.4.1 supertest
```

Add a test script to the package.json file:

```json
{
  "scripts": {
    "test": "mocha  --exit"
  }
}
```

### Δημιουργία του αρχείου Testing

Δημιουργήστε έναν κατάλογο `test` και ένα αρχείο `posts.test.js` μέσα σε αυτόν.

```bash
mkdir test
touch test/posts.test.js
```

### Συγγραφή Tests

#### `test/posts.test.js`

```javascript
const request = require('supertest');
const chai = require('chai');
const app = require('../app'); // Import the Express application
const expect = chai.expect;

describe('Blog API', function() {
  describe('GET /posts', function() {
    it('should return all posts', async function() {
      const response = await request(app).get('/posts');
      expect(response.status).to.equal(200);
      expect(response.body).to.be.an('array');
      expect(response.body.length).to.be.greaterThan(0);
    });
  });

  describe('POST /posts', function() {
    it('should create a new post', async function() {
      const newPost = { title: 'New Post', content: 'This is a new post' };
      const response = await request(app).post('/posts').send(newPost);
      expect(response.status).to.equal(201);
      expect(response.body).to.include.keys('id', 'title', 'content');
      expect(response.body.title).to.equal(newPost.title);
    });
  });

  describe('PUT /posts/:id', function() {
    it('should update an existing post', async function() {
      const updatedPost = { title: 'Updated Post', content: 'This is an updated post' };
      const response = await request(app).put('/posts/1').send(updatedPost);
      expect(response.status).to.equal(200);
      expect(response.body).to.include.keys('id', 'title', 'content');
      expect(response.body.title).to.equal(updatedPost.title);
    });
  });

  describe('DELETE /posts/:id', function() {
    it('should delete an existing post', async function() {
      const response = await request(app).delete('/posts/1');
      expect(response.status).to.equal(204);
    });
  });
});

```

### Εκτέλεση Tests

Εκτελέστε τις δοκιμές χρησιμοποιώντας το Mocha:

```bash
npm test
```

## Έλεγχος Test Coverage

Ελέγχουμε πόσος κώδικας καλύπτεται από δοκιμές χρησιμοποιώντας το εργαλείο `nyc`.

### Εγκατάσταση `nyc`

Εγκαταστήστε το `nyc` για να μετρήσετε την κάλυψη κώδικα:

```bash
npm install --save-dev nyc
```

### Ρύθμιση `nyc` 

Προσθέστε τις ρυθμίσεις nyc στο αρχείο `package.json`:

```json
{
  "scripts": {
    "test": "nyc mocha --exit"
  },
  "nyc": {
    "reporter": [
      "text",
      "html"
    ],
    "exclude": [
      "test/**"


    ]
  }
}
```

Εκτελέστε δοκιμές με το `nyc` για να δείτε την κάλυψη:

```bash
npm test
```

Δείτε την αναφορά HTML στον κατάλογο `coverage` για λεπτομερείς πληροφορίες κάλυψης.
