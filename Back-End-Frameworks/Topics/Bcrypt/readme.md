# Bcrypt

In this section, we will discuss `bcrypt`, which is a hashing function primarily used for hashing passwords.



## Learning Outcomes

By the end of this section, students should be able to:

- Explain what `bcrypt` is and how to use it.
- List the advantages of using `bcrypt`.
- Implement `bcrypt` for hashing and comparing passwords.

## What is Bcrypt?

`Bcrypt` is a hashing function used primarily for hashing passwords. Hashing is the process of transforming an input value (e.g., a password) into a fixed-length output known as a hash value. The hash value is unique and cannot be reverted to the original input. Hashing is commonly used to ensure data security, as it is unique and irreversible.

Hashing is often confused with encryption, but they are two different processes. Encryption is the process of transforming an input value into an encrypted output using a cryptographic key, which can then be decrypted back to the original input. In contrast, a hashed value cannot be converted back to the original input, making it more secure for storing sensitive data.

## Advantages of Bcrypt

- **Security**: Unlike many other hashing functions, `bcrypt` is designed to be slow, making it more difficult for attackers to brute-force passwords. The slowness can be adjusted by increasing or decreasing the number of salt rounds.

- **Salting**: `Bcrypt` automatically includes a salting feature. Salting means adding random data to a password before hashing it to prevent duplicate hash values for the same passwords and make it more difficult for attackers using precomputed hash tables (known as "rainbow tables").

## Using Bcrypt

When implementing bcrypt in an API, the workflow generally involves hashing the password before storing it in the database and then comparing the hashed password during user login.

To install `bcrypt`, use the command:

```bash
npm install bcrypt
```

A sample hashing service might look like this:

```javascript
// Import bcrypt
const bcrypt = require("bcrypt");
// This variable determines how much work to do for password hashing
// The higher the number, the more effort is required
const saltRounds = 10;

const hashService = {
  // Function to hash a password - returns the hashed password
  hash: async (password) => {
    const hash = await bcrypt.hash(password, saltRounds);
    return hash;
  },
  // Function to compare a password with a hash - returns true or false based on the comparison result
  compare: async (password, hash) => {
    const match = await bcrypt.compare(password, hash);
    return match;
  },
};

// Exporting the created object for use in other modules
module.exports = hashService;
```

Now we can use this service when creating, updating, or logging in users.

Hashing a password during user creation might look like this:

```javascript
createUser: async (newUser) => {
  const id = db.users.length + 1;
  // Hash the new user's password
  const hashedPassword = await hashService.hash(newUser.password);
  // Add the user to the 'database' with the hashed password
  db.users.push({
    id,
    ...newUser,
    password: hashedPassword,
  });
  return id;
},
```

User login and password comparison might look like this:

```javascript
login: async (email, password) => {
  // Find the user by email
  const user = db.users.find((user) => user.email === email);
  // If the user is not found, return an error message
  if (!user) {
    return 'User not found';
  }
  // Compare the entered password with the hashed password
  const match = await hashService.compare(password, user.password);
  // If the passwords do not match, return an error message
  if (!match) {
    return 'Incorrect password';
  }
  // If the passwords match, return user details
  return user;
},
```

## Summary

`Bcrypt` is a secure hashing function that can be used for hashing and comparing passwords. Its slowness and automatic salting make it more secure than other hashing functions. Using `bcrypt` helps protect user passwords and ensure their privacy in web applications.

## Sources

- [Bcrypt npm page](https://www.npmjs.com/package/bcrypt)
- [Wikipedia](https://en.wikipedia.org/wiki/Bcrypt#:~:text=The%20bcrypt%20function%20is%20the,Ruby%2C%20python%20and%20other%20languages.)
