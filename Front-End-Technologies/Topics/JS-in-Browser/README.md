# Javascript in Browser

In this topic we'll learn about Javascript in browser and how to include Javascript in HTML files.

- [Javascript in Browser](#javascript-in-browser)
  - [Learning Outcomes](#learning-outcomes)
  - [Difference between Node.js and Browser Javascript](#difference-between-nodejs-and-browser-javascript)
  - [Including Javascript in HTML](#including-javascript-in-html)
    - [Using `<script>` tag](#using-script-tag)
    - [Using `src` attribute](#using-src-attribute)
  - [Input and Output in Browser Javascript](#input-and-output-in-browser-javascript)
    - [`prompt()` function](#prompt-function)
    - [`alert()` function](#alert-function)
  - [Exercises](#exercises)
    - [Exercise 1: Basic User Greeting](#exercise-1-basic-user-greeting)
    - [### Exercise 2: Simple Math Quiz](#-exercise-2-simple-math-quiz)
    - [Exercise 3: Age Category Checker](#exercise-3-age-category-checker)


## Learning Outcomes

After completing this topic, you'll be able to:

- Describe the difference between Node.js and browser Javascript.
- Include Javascript in HTML.
- Get user input and display output in browser Javascript.
- Use `prompt()` and `alert()` functions.

## Difference between Node.js and Browser Javascript

Main difference is that Node.js is a Javascript runtime environment, while browser Javascript is a Javascript engine. Javascript engine is a program that executes Javascript code. Javascript runtime environment is a program that executes Javascript code and provides additional features, such as access to the file system, network, etc.

For example, Javascript in browser cannot access the file system, while Node.js can. Javascript in browser can access the DOM, while Node.js cannot.

There are different global objects in Node.js and browser Javascript. For example, `window` an `document` objects are available in browser Javascript, but not in Node.js. `process` object is available in Node.js, but not in browser Javascript.

- `window` object is the global object in browser Javascript. It represents the browser window. It has properties and methods that allow to access the browser window and its content.
- `document` object is the global object in browser Javascript. It represents the DOM. It has properties and methods that allow to access the DOM and its content.
- `process` object is the global object in Node.js. It has properties and methods that allow to access the Node.js process and its content.

Javascript syntax is the same in both environments.

## Including Javascript in HTML

Browsers can execute Javascript code that is included in HTML files. There are two ways to include Javascript code in HTML files:

- using `<script>` tag;
- using `src` attribute.

### Using `<script>` tag

Javascript code can be included in HTML files using `<script>` tag. `<script>` tag can be placed in the `<head>` or `<body>` section of the HTML file. Javascript code that is included in the `<head>` section is executed before the HTML file is loaded. Javascript code that is included in the `<body>` section is executed after the HTML file is loaded.

```html
<!DOCTYPE html>
<html>
<head>
    <title>Page Title</title>
    <script>
        console.log('Hello, world!');
    </script>
</head>
<body>
    <h1>My First Heading</h1>
    <p>My first paragraph.</p>
</body>
</html>
```
> Note: in browser Javascript, we can see the output of `console.log()` in the browser console. To open the browser console, press `F12` or `Ctrl+Shift+I` in Chrome, Firefox, or Edge.
> ![Console](Console.png)

### Using `src` attribute

Javascript code can be included from external Javascript files using `src` attribute. `src` attribute can be used with `<script>` tag. Javascript code that is included using `src` attribute is executed after the HTML file is loaded.

```html
<!DOCTYPE html>
<html>
<head>
    <title>Page Title</title>
    <script src="script.js"></script>
</head>
<body>
    <h1>My First Heading</h1>
    <p>My first paragraph.</p>
</body>
</html>
```

## Input and Output in Browser Javascript

There are several ways to get user input and display output in browser Javascript. Main interactions with the user are done using the DOM. Using DOM we can read and modify the content of HTML elements like different input elements, paragraphs, headings, etc. But for the first steps, we can use `prompt()` and `alert()` functions.

### `prompt()` function

`prompt()` function displays a dialog box that prompts the user for input. It takes one argument, which is the text to display in the dialog box. It returns the text that the user entered in the dialog box.

```js
let name = prompt('Enter your name:');
console.log('Hello, ' + name + '!');
```

### `alert()` function

`alert()` function displays a dialog box that shows a message to the user. It takes one argument, which is the text to display in the dialog box.

```js
alert('Hello, world!');
```

Usually we don't use `prompt()` and `alert()` functions in browser Javascript and we use the DOM instead. But they are useful for the first steps.

## Exercises

Write a Javascript code into a separate file and include it in an HTML file using `src` attribute.

Try to solve exercises without looking at the solution. If you get stuck, you can look at the solution.

Always test your code to see if it works as expected.

### Exercise 1: Basic User Greeting

**Objective**: Prompt the user for their name and greet them with a personalized message.

**Description**: Write a JavaScript script that uses `prompt` to ask the user for their name. Then, use `alert` to display a greeting message that includes their name.

**Expected Behavior**: The browser first displays a prompt for the user's name and then shows an alert with a greeting message using the provided name.

<details>

<summary>Solution</summary>
`app.js`:

```js
// Use prompt to ask the user's name and store it in a variable
const userName = prompt('What is Your name?');

// Use alert to display a greeting message
alert(`Hello, ${userName}!`);
```

`index.html`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Greeting page</title>
    <script src="app.js"></script>
</head>
<body>
    <h1>This is greeting page</h1>
</body>
</html>
```
![Prompt and Alert](PromptAndAlert.gif)
</details>

### ### Exercise 2: Simple Math Quiz

**Objective**: Ask the user a basic math question and provide feedback based on their answer.

**Description**: Use `prompt` to ask the user a simple math question (e.g., "What is 2 + 3?"). Check if the answer is correct. Use `alert` to give them appropriate feedback. If they are correct, display a congratulatory message; if incorrect, display the correct answer.

**Expected Behavior**: The user is prompted to answer a math question and then receives feedback based on their response.

<details>
<summary>Solution</summary>

`app.js`:

```js
// Ask a simple math question
const userAnswer = prompt('What is 2 + 3?');

// Check the answer and provide feedback
if (parseInt(userAnswer) === 5) {
    alert('Correct! Well done.');
} else {
    alert('Incorrect. The correct answer is 5.');
}
```

> Note: `parseInt()` function converts a string to an integer. For example, `parseInt('5')` returns `5`. We should use `parseInt()` function because `prompt()` function returns a string.

`index.html`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Math Quiz</title>
    <script src="app.js"></script>
</head>
<body>
    <h1>This is math quiz</h1>
</body>
</html>
```
</details>

### Exercise 3: Age Category Checker

**Objective**: Determine the user's age category based on the age they enter.

**Description**: Use `prompt` to ask the user for their age. Depending on the age they enter, use `alert` to inform them of their age category (e.g., child, teenager, adult).

**Expected Behavior**: The user is asked for their age and receives an alert indicating their age category.
