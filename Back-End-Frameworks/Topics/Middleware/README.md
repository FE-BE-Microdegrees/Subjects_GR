 # Middleware in Express

In this section, we will discuss middleware in the context of Express.js.

![Middleware](Middleware.webp)

Image source: Dall-E by OpenAI

- [Middleware in Express](#middleware-in-express)
  - [Learning Outcomes](#learning-outcomes)
  - [What are Middleware Functions?](#what-are-middleware-functions)
  - [Next Function](#next-function)
  - [Using Middleware](#using-middleware)
    - [Example of Logging Middleware](#example-of-logging-middleware)
  - [Request/Response Cycle with Middleware](#requestresponse-cycle-with-middleware)
  - [Not Found Middleware](#not-found-middleware)
    - [Registering Not Found Middleware](#registering-not-found-middleware)

## Learning Outcomes

By the end of this section, you will be able to:

- Explain what middleware is and how it is used.
- Write middleware functions.
- Implement middleware in an Express.js application.

## What are Middleware Functions?

Middleware functions are functions that have access to the request object (`req`), response object (`res`), and the next middleware function in the application's request-response cycle. Essentially, you can think of middleware as a filter that processes requests before they reach the next stage in the request-response cycle. For example, middleware could handle logging, authentication, request data parsing, or any other functionality that is important for the application.

## Next Function

The `next` function is an Express router function that, when called, passes control to the next middleware in the stack.

## Using Middleware

Middleware can:

- Execute code.
- Modify the request and response objects.
- End the request-response cycle.
- Call the next middleware in the stack.

It’s important to remember that if a middleware does not end the request-response cycle (e.g., using `return res.status(200).json…`), it must call the `next()` function; otherwise, the application will hang.

### Example of Logging Middleware

```javascript
// Middleware for logging HTTP requests

const logger = (req, res, next) => {
  // Log the request URL, method, and time
  console.log(req.url, req.method, new Date().toISOString());
  // Call the next middleware
  return next();
};
```

Middleware can be applied in different ways.

One option is to register the middleware for all requests:

```javascript
...
// Importing middleware (path depends on file location)
const logger = require('./middlewares/logger');

...

// Registering middleware
app.use(logger);

...
```

Another option is to register middleware only for specific routes:

```javascript
...
// Importing middleware
const logger = require('./middlewares/logger');

...

// Registering middleware
app.get('/api', logger, (req, res) => {
  res.send('Hello World!');
});
...
```

## Request/Response Cycle with Middleware

![Middleware Cycle](./middleware.png)

## Not Found Middleware

One useful scenario for middleware is displaying a 404 page when the requested resource is not found. Example:

```javascript
// Middleware to display a 404 page when the requested resource is not found

const notFound = (req, res, next) => {
  res.status(404).send({
    success: false,
    message: "Route not found",
  });
};

module.exports = notFound;
```

### Registering Not Found Middleware

```javascript
...
// Importing middleware
const notFound = require('./middlewares/notFound');

...

// Registering middleware
app.use('*', notFound);

...
```

Here, it is important to register this middleware after all routes, using the path `*`. This means that if a user accesses a route that does not exist in the API, they will be directed to this middleware function.

Now, if a user tries to access a route that does not exist, they will receive the following response:

```json
{
  "success": false,
  "message": "Route not found"
}
```
