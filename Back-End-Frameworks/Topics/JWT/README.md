# JWT (_JSON Web Token_)

In this section, we will discuss JWT (_JSON Web Token_), an open standard used for securely transmitting data between parties in JSON format.

![JWT](JWT.webp)

Image source: DALL-E by OpenAI

## Learning Outcomes

By the end of this section, students should be able to:

- Explain what JWT is and how it works.
- Describe the structure of JWT and its components.
- Create and validate JWTs.
- Use JWTs in authentication and authorization processes.

## JWT

JWT (_JSON Web Token_) is an open standard (RFC 7519) used for securely transmitting data between parties in JSON format. It is particularly useful for authentication and information exchange, allowing reliable and efficient information transfer. JWTs are compact and easy to use in various scenarios, including authentication and authorization in web applications.

### JWT Components

A JWT consists of three parts, separated by periods (.):

- **Header:** Contains information about the type of token and the signing algorithm being used (e.g., HMAC SHA256 or RSA).

```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

- **Payload:** Contains claims, which are the encoded information in the JWT. Claims can be standardized, public, or private.

```json
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true
}
```

- **Signature:** Created to ensure the integrity and authenticity of the token. The signature is generated using a secret key or a public/private key pair.

```bash
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret
)
```

### JWT Structure

The complete JWT structure looks like this:

```bash
xxxxx.yyyyy.zzzzz
```

Where `xxxxx` is the header, `yyyyy` is the payload, and `zzzzz` is the signature, all encoded in base64-url.

## When to Use JWT?

- **Authorization:** This is the most common scenario for using JWTs. Once a user logs in, each subsequent request contains a JWT, allowing the user to access the routes, services, and resources authorized for that token.
- **Information Exchange:** JSON Web Tokens are a good way to securely transmit information between parties. Since JWTs can be signed, for example, using public/private key pairs, you can be sure the senders are who they say they are. Additionally, because the signature is computed using the header and payload, you can also verify that the content has not been altered.

### Advantages

- **Compactness:** JWTs are compact, meaning they can be easily transmitted via URLs, HTTP headers, and POST data.
- **Self-Contained:** Tokens are self-contained as they contain all the necessary information. You can validate the token without additional data, making the system more efficient and flexible.
- **Security:** JWTs ensure data integrity and enable authentication and authorization, which is useful for establishing secure connections.

### Disadvantages

- **Token Leakage:** JWTs cannot be revoked or invalidated once issued. If a JWT is leaked, it can be dangerous as it may grant unauthorized access, necessitating additional protective measures.

## Creating and Validating JWTs

### Creating JWTs

The process of creating a JWT involves generating the header, payload, and signature, then combining them.

#### Example in Node.js

To create and validate JWTs in Node.js, you can use the `jsonwebtoken` library.

- **Install the jsonwebtoken library:**

```bash
npm install jsonwebtoken
```

- **Creating a JWT:**

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

### Validating JWTs

Validating a JWT involves decoding the received token and verifying the signature to ensure its authenticity and integrity.

#### Example in Node.js

1. **Validating a JWT:**

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

## Using JWT for Authentication and Authorization

### Authentication

JWTs are often used for user authentication. When a user logs in, the server creates a JWT containing the user's identity and possible permissions. This JWT is sent back to the user and stored in the browser as a cookie or in local storage.

#### Example - 1

- **User Login and JWT Creation:**

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

### Authorization

Once a user is authenticated and has a JWT, the server can use that token to check the user's identity and permissions when they request protected resources.

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
