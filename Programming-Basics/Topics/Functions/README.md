# Functions

In this topic, we will learn about functions in Javascript.

- [Functions](#functions)
  - [Learning Outcomes](#learning-outcomes)
  - [What is a Function?](#what-is-a-function)
  - [Function Declaration](#function-declaration)
  - [Function Expression](#function-expression)
  - [Function Invocation](#function-invocation)
  - [Function Scope](#function-scope)
  - [Function Hoisting](#function-hoisting)
  - [Arrow Functions](#arrow-functions)
  - [Exercises](#exercises)
    - [Exercise 1 - Basic Function Definition and Call](#exercise-1---basic-function-definition-and-call)
    - [Exercise 2 - Function with Return Value](#exercise-2---function-with-return-value)
    - [Exercise 3 - Function Manipulating Array Data](#exercise-3---function-manipulating-array-data)

## Learning Outcomes

After completing this topic, you'll be able to:

- Define what a function is
- Explain the difference between function declaration and function expression
- Explain what function invocation is
- Explain what function scope is
- Explain what function hoisting is
- Explain what arrow functions are

## What is a Function?

A function is a block of code that performs a specific task. Functions are used to organize code into logical units that can be reused in other parts of the program.

Function consist (and can consist) of the following parts:

- keyword to declare a function
- name of the function
- parameters of the function (optional)
- function body
- return statement (optional)
- return value (optional)

```javascript
function add(a, b) {
  const sum = a + b;
  return sum;
}
```

In previous example, we declared a function named `add` with keyword `function`, that takes two parameters `a` and `b` and returns the sum of `a` and `b`. The function body consists of two statements: `const sum = a + b;` and `return sum;`. The first statement declares a variable named `sum` and assigns the value of `a + b` to it. The second statement returns the value of `sum` variable.

> We should remember, that parameters are variables that are used to store values that are passed to the function when it is called. If we don't need to pass any values to the function, we can omit the parameters. For example, if we want to declare a function named `sayHello` that prints the words "Hello World!" to the console, we can declare it like this:

```javascript
function sayHello() {
  console.log('Hello World!');
}
```

> Next important thing to remember is that function always returns a value. If we don't specify the return value, the function will return `undefined`. In our previous `sum` function, we specified the return value using the `return` keyword. If we don't specify the return value (like in `sayHello` function), the function will return `undefined`. 

In Javascript we can declare functions in two ways: function declaration and function expression.

## Function Declaration

For function declaration, we use the `function` keyword followed by the name of the function, optional parameters, and function body. Similarily to previous examples, we declare functions like this:

```javascript
function functionName(parameter1, parameter2) {
  // function body
  return value;
}
```

## Function Expression

But we can also declare functions using function expressions. For function expression, we use the `const` keyword followed by the name of the function, optional parameters, and function body. It means, that we declare function and assign it to a variable. For example:

```javascript
const add = function(a, b) {
  const sum = a + b;
  return sum;
}
```

Even though we use the `const` keyword to declare the function, we can still call the function using the function name followed by parentheses. For example:

```javascript
const sum = add(1, 2);

console.log(sum); // 3
```

## Function Invocation

To execute a function, we need to call it. We can call a function by using the function name followed by parentheses. For example, if we want to call the `add` function, we can type `add(1, 2);` in the code. This will call the `add` function with the values `1` and `2` as arguments. The function will return the sum of `1` and `2` and we can store the return value in a variable like this:

```javascript
const sum = add(1, 2);

console.log(sum); // 3
```

If we don't store the return value in a variable, the return value will be lost. For example, if we call the `add` function like this:

```javascript
add(1, 2);
```

The function will return the sum of `1` and `2`, but we won't be able to store the return value. The return value will be lost.

## Function Scope

The scope of a variable is the part of the program where the variable can be accessed. In Javascript, there are two types of scope: **global scope** and **local scope**. A variable that is declared outside of a function has a **global scope** and can be accessed anywhere in the program. A variable that is declared inside of a function has a **local scope** and can only be accessed inside of the function.

For example, if we declare a variable named `x` outside of a function, we can access it anywhere in the program. For example:

```javascript
let x = 5; // declare a variable named x and assign the value 5 to it

function printX() {
  console.log(x); // print the value of the x variable to the console
}

printX(); // 5
```

In this example, we declared a variable named `x` outside of a function and assigned the value `5` to it. We also declared a function named `printX` that prints the value of the `x` variable to the console. We called the `printX` function and it printed the value of the `x` variable to the console.

But if we declare a variable named `x` inside of a function, we can only access it inside of the function. For example:

```javascript
function printX() {
  let x = 5; // declare a variable named x and assign the value 5 to it
  console.log(x); // print the value of the x variable to the console
}

printX(); // 5

console.log(x); // ReferenceError: x is not defined
```

In this example, we declared a function named `printX` that declares a variable named `x` and assigns the value `5` to it. We also declared a function named `printX` that prints the value of the `x` variable to the console. We called the `printX` function and it printed the value of the `x` variable to the console. But if we try to access the `x` variable outside of the `printX` function, we will get a `ReferenceError` because the `x` variable is not defined outside of the `printX` function.

## Function Hoisting

Function hoisting is a Javascript mechanism that moves function declarations to the top of the current scope. This means that we can call a function before it is declared. For example:

```javascript
printX(); // 5

function printX() {
  let x = 5; // declare a variable named x and assign the value 5 to it
  console.log(x); // print the value of the x variable to the console
}
```

In this example, we called the `printX` function before it was declared. This is possible because of function hoisting. Function hoisting moves the function declaration to the top of the current scope, so we can call the function before it is declared.

But we have to rememeber, that function hoisting only works with function declarations, not with function expressions. For example:

```javascript
printX(); // TypeError: printX is not a function

const printX = function() {
  let x = 5; // declare a variable named x and assign the value 5 to it
  console.log(x); // print the value of the x variable to the console
}
```

In this example, we tried to call the `printX` function before it was declared. But we got a `TypeError` because function hoisting only works with function declarations, not with function expressions.

So basically, it is a good practice to declare functions before we call them, but we can call functions before they are declared because of function hoisting.

## Arrow Functions

Arrow functions are a new way to declare functions in Javascript. They are similar to function expressions, but they have a shorter syntax. For example, if we want to declare a function named `add` that takes two parameters `a` and `b` and returns the sum of `a` and `b`, we can declare it like this:

```javascript
const add = (a, b) => {
  const sum = a + b;
  return sum;
}

const result = add(1, 2);
console.log(result); // 3
```

In this example we declared a function using arrow function syntax. We can see, that the arrow function syntax is bit different and shorter, but calling the function is the same as with function expressions.

## Exercises

Create a file named index.js (or another name of your choice) and start adding solutions to the exercises below.

Test your code by running the index.js file using the node index.js command.

Test your code with different values

### Exercise 1 - Basic Function Definition and Call

**Objective**: Write a function that prints a greeting message.

**Description**: Define a function named greet that takes a name as an argument and prints "Hello, [name]!". Call this function with a name.

<details>
  <summary>Solution</summary>

```javascript
function greet(name) {
  console.log(`Hello, ${name}!`);
}

greet('John');
```

**Expected output**:

```javascript
Hello, John!
```
![Function](function.gif)

</details>

### Exercise 2 - Function with Return Value

**Objective**: Create a function that calculates and returns the area of a rectangle.

**Description**: Write a function named `calculateArea` that takes the `length` and `width` of a rectangle as arguments and returns its area. Call this function with different sets of values and print the results.

> Hint: You can give multiple arguments to a function by separating them with commas.
> 
> Hint: The area of a rectangle is calculated by multiplying its length by its width.

<details>
  <summary>Solution</summary>

```javascript
function calculateArea(length, width) {
  const area = length * width;
  return area;
}

const area1 = calculateArea(5, 10);
console.log(area1);

const area2 = calculateArea(2, 4);
console.log(area2);
```

**Expected output**:

```javascript
50
8
```
</details>

### Exercise 3 - Function Manipulating Array Data

**Objective**: Write a function that filters even numbers from an array and returns a new array.

**Description**: Define a function named `filterEvenNumbers` that takes an array of numbers as an argument. This function should return a new array containing only the even numbers from the original array.

> Hint: You can use the modulus operator (%) to check if a number is even or odd. If a number is even, the result of the modulus operation will be 0. If a number is odd, the result of the modulus operation will be 1.
>
> Hint: You can use the push() method to add an element to the end of an array.

**Example**:

```javascript
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9];

const evenNumbers = filterEvenNumbers(numbers);

console.log(evenNumbers);
```

**Expected output**:

```javascript
[2, 4, 6, 8]
```
