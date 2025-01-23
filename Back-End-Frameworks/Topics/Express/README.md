# Express

In this lesson, we will explore Express, a popular web application framework for Node.js. We will learn how to install Express, use its methods, and work with request and response objects in Express.

![Express](Express.webp)

Image source: Dall-E by OpenAI

- [Express](#express)
  - [Learning Outcomes](#learning-outcomes)
  - [What is Express?](#what-is-express)
  - [Installing Express](#installing-express)
  - [Express App Methods](#express-app-methods)
  - [Request and Response in Express](#request-and-response-in-express)
    - [Sources](#sources)

## Learning Outcomes

By the end of this lesson, you will be able to:

- Explain what Express is and why it is used.
- Install Express in a Node.js project.
- Create a simple Express application and run it.

## What is Express?

Express is a popular web application framework for Node.js, designed for building scalable and flexible web applications. It provides a range of features for developing web applications, such as routing, middleware, and support for handling HTTP requests and responses.

Express simplifies the process of building web applications by offering a lightweight yet powerful framework that allows developers to focus on creating core application functionality. It includes a simple API that enables developers to easily create HTTP routes, define middleware functions to handle requests, and work with various templating engines and other tools.

## Installing Express

To install Express in a Node.js project, follow these steps:

1. Create a new directory for your project and navigate to that directory in the terminal.
2. Initialize a new Node.js project using the command `npm init`. This will create a `package.json` file that tracks your project's dependencies.
3. Install Express using the command `npm install express`. This will download and install the latest version of Express and its dependencies.

Here is an example of installing Express using the command line:

```bash
mkdir myapp
cd myapp
npm init -y
npm install express
```

After installing Express, you can create a new file named `app.js` and start building your application using the Express framework. To use Express in your application, you need to import it in your `app.js` file like this:

```javascript
const express = require("express");
const app = express();
```

Here’s a simple example of an Express application:

```javascript
const express = require("express");
const app = express();

const port = 3000;

app.get("/", (req, res) => {
  return res.send("Hello!");
});

app.listen(port, () => {
  console.log(`Listening on port: ${port}`);
});
```

## Express App Methods

Similar to [HTTP request methods](../http-methods/README.md), Express provides a wide range of methods that can be used to create web applications and receive requests from clients. Here are some of the most common methods in an Express application:

- **GET**: (`app.get()`) This method is used to retrieve data from the server. It is used to request a specific resource, such as a webpage, image, or video.

- **POST**: (`app.post()`) This method is used to send data to the server. It is typically used to submit forms or send data to the server for processing.

- **PUT**: (`app.put()`) This method is used to update existing data on the server. It is typically used to update a specific resource (e.g., a user profile or product information).

- **DELETE**: (`app.delete()`) This method is used to delete data from the server. It is typically used to remove a specific resource, such as a user account or product.

- **USE**: (`app.use()`) This method is used to define middleware functions that execute for every request that matches a specific route.

- **SET**: (`app.set()`) This method is used to set application-level variables (e.g., port number or view engine).

These are just a few of the many methods offered by Express. Each method can be used to create routes that handle specific types of HTTP requests, enabling developers to build powerful and flexible web applications.

## Request and Response in Express

Similar to the HTTP protocol, Express provides options for receiving and sending request and response objects.

When a request is received, Express creates its version of the request, which has many different properties, including:

- **params**: (req.params) This attribute is an object containing parameters matched to the named route "parameters." For example, if you have a route `/users/:id`, the params object will have the attribute `id` with the value `:id`.

- **query**: (req.query) This attribute is an object containing attributes for each query string parameter of the route. For example, if the URL is `/users?sort=desc`, the request object will contain `{ sort: 'desc' }`.

- **body**: (req.body) This attribute is an object containing the parsed body of the request when the request method is `POST`, `PUT`, or `PATCH`, and the content-type header is `application/x-www-form-urlencoded` or `application/json`.

- **headers**: (req.headers) This attribute is an object containing the headers sent by the client.

- **method**: (req.method) This attribute is a string that contains the HTTP request method (e.g., `GET`, `POST`, `PUT`, `DELETE`, etc.).

- **url**: (req.url) This attribute is a string that contains the request URL.

- **cookies**: (req.cookies) This attribute is an object that contains cookies sent by the client.

- **ip**: (req.ip) This attribute is a string that contains the client's IP address.

- **protocol**: (req.protocol) This attribute is a string that contains the protocol used for the request (http or https).

Overall, the Express request object provides developers with a wealth of information about the client's request, enabling them to create powerful and flexible web applications.

To send a response, Express offers several functions, the most common of which are:

- **send**: (res.send()) This method is used to send a string, buffer, or JSON response back to the client. It automatically sets the `Content-Type` header based on the type of data.

- **json**: (res.json()) This method is used to send a JSON response back to the client. It sets the `Content-Type` header to `application/json`.

- **redirect**: (res.redirect()) This method is used to redirect the client to another URL. It sets the location header to the specified URL and defaults to the `302` status code.

- **render**: (res.render()) This method is used to render a view template and send an HTML response back to the client. It takes the name of the template and a data object as arguments.

- **status**: (res.status()) This method is used to set the HTTP response status code. It can be used to specify any valid HTTP status code.

- **sendFile**: (res.sendFile()) This method is used to send a file in response. It takes the file path as an argument and automatically sets the content-type header based on the file extension.

These are just a few of the many response methods offered by Express. Each method can be used to send different types of responses back to the client.

### Sources

- [Express Official Website](https://expressjs.com/)
- [Express API Reference](https://expressjs.com/en/4x/api.html#app.METHOD)
- [Request Object in Express](https://expressjs.com/en/api.html#req)
- [Response Object in Express](https://expressjs.com/en/api.html#res)
