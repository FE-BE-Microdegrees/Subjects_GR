# Variables

In this topic, we'll learn about variables in Javascript.

- [Variables](#variables)
  - [Learning Outcomes](#learning-outcomes)
  - [What is a Variable?](#what-is-a-variable)
  - [How to Declare a Variable?](#how-to-declare-a-variable)
  - [Assigning Values to Variables](#assigning-values-to-variables)
  - [Exercises](#exercises)
    - [Exercise 1](#exercise-1)
    - [Exercise 2](#exercise-2)
    - [Exercise 3](#exercise-3)

## Learning Outcomes

After completing this topic, you'll be able to:
- Define what a variable is
- Declare variables
- Assign values to variables
- Explain the difference between `var`, `let`, and `const`

## What is a Variable?

A variable is a named storage location in a computer's memory that can be used to store data. Variables are used to store values that can be changed during the execution of a program. For example, a variable named `x` can be used to store the value `5`. The value of `x` can be changed to `10` by assigning the value `10` to `x`. Variables are used to store data that can be used later in the program.

We can imagine a variable as a box with a label on it (`variable name`) that can contain something (`value`). We can put something in the box (`assign a value`) and we can take something out of the box (`use the value`). If we want to know what is in the box, we can look at the label (`variable name`) to identify the box and then open the box to see what is inside (`access the value`).

For example, we could have `apples` variable, which contains some apples. If we want to know how many apples we have in the `apples` variable, we can look at the label (`apples`) to identify the box and then open the box to see how many apples are inside (`access the value`).

In Javascript it would be something like this:

```javascript
let apples = 5; // declare a variable named apples and assign the value 5 to it (put 5 apples in the box)
console.log(apples); // print the value of the apples variable to the console (open the box, see how many apples are inside and print the value to the console)
```

## How to Declare a Variable?

In order to use a variable in a program, we must first declare it. In Javascript, we can declare a variable using the `var`, `let`, or `const` keywords.
- The `var` keyword is used to declare a variable that can be reassigned, but we should avoid using `var` nowadays and use `let` instead.
- The `let` keyword is used to declare a variable that can be reassigned.
- The `const` keyword is used to declare a variable that cannot be reassigned.

```javascript
let firstName; // declare a variable named x
let age, lastName; // declare multiple variables 
```

In previous example, we declared variables named `firstName`, `age`, and `lastName`. We can also declare variables and assign values to them at the same time.

## Assigning Values to Variables

We can assign values to variables using the assignment operator `=`. The value on the right side of the assignment operator is assigned to the variable on the left side of the assignment operator.

```javascript
let firstName = 'John'; // declare a variable named firstName and assign the value 'John' to it
let age = 25, lastName = 'Doe'; // declare multiple variables and assign values to them
const PI = 3.14; // declare a constant named PI and assign the value 3.14 to it
```

## Exercises

Create a file named `index.js` (or another name of your choice) and start adding solutions to the exercises below.

Test your code by running the `index.js` file using the `node index.js` command.

You can also test Your code with different values for the variables.

### Exercise 1

Declare a variable named `firstName` and assign the value `John` to it.

Print the value of the `firstName` variable to the console.

Test your code by running the `index.js` file using the `node index.js` command.

<details>
  <summary>Solution</summary>

```javascript
let firstName = 'John'; // declare a variable named firstName and assign the value 'John' to it

console.log(firstName); // print the value of the firstName variable to the console
```
![Declaring variable with value](DeclaringVariableWithValue.gif)

</details>

### Exercise 2

In the same file, declare a variable named `lastName` and assign the value `Doe` to it.

Print out values of the `firstName` and `lastName` variables in a single line. Output should look like this: `John Doe`.

Test your code by running the `index.js` file using the `node index.js` command.

> Hint: Use the `+` operator to concatenate the values of the `firstName` and `lastName` variables.

<details>
  <summary>Solution</summary>

```javascript
let firstName = 'John'; // declare a variable named firstName and assign the value 'John' to it
let lastName = 'Doe'; // declare a variable named lastName and assign the value 'Doe' to it

console.log(firstName + ' ' + lastName); // print out values of the firstName and lastName variables in a single line
```

</details>

### Exercise 3

In the same file, declare a variable named `age` and assign the value `25` to it.

Print out text `John is 25 years old.` using the `firstName` and `age` variables.
