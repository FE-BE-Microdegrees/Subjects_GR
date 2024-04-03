# Data Types

In this topic, we'll learn about data types in Javascript.

- [Data Types](#data-types)
  - [Learning Outcomes](#learning-outcomes)
  - [What is a Data Type?](#what-is-a-data-type)
  - [Primitive Data Types](#primitive-data-types)
  - [Object Data Types](#object-data-types)
  - [Type Conversion](#type-conversion)
  - [Type Coercion](#type-coercion)
  - [Exercises](#exercises)
    - [Exercise 1](#exercise-1)
    - [Exercise 2](#exercise-2)

## Learning Outcomes

After completing this topic, you'll be able to:
- Define what a data type is
- List the primitive data types in Javascript
- List the object data types in Javascript
- Convert values from one data type to another
- Explain the difference between type conversion and type coercion

## What is a Data Type?

As we already know, the variable is a `named storage location in a computer's memory` that can be used to store data. The data that can be stored in a variable has a *type*. The **type** of data determines what operations can be performed on it. For example, we can add two **numbers** together, but we cannot add a **number** and a **string** together.

Javascript is a dynamically typed language, which means that the **type** of a variable can be changed throughout the execution of a program. For example, we can assign a **number** to a variable and then assign a **string** to the same variable later in the program. This is different from statically typed languages like Java, where the type of a variable is fixed as we declare it.

In Javascript, we can divide data types into two categories: 
- **primitive data** types
- **object data** types.

## Primitive Data Types

Primitive data types are the most basic data types in Javascript. There are 7 primitive data types in Javascript:

- **String**: a sequence of *characters* enclosed in single or double quotes
- **Number**: a *numeric* value
- **Boolean**: a value that is either *true* or *false*
- **Undefined**: a value that represents *lack of value* (e.g., when a variable is declared but has not been assigned a value)
- **Null**: a value that represents *nothing* (the difference from *undefined* value is usually that *null* is a deliberately assigned value)
- **Symbol**: a *unique* value used to identify object properties (we will not use this type in this course)
- **BigInt**: a numeric value that is *larger than Number.MAX_SAFE_INTEGER* (we will not use this type in this course)

```javascript
let firstName = 'John'; // string
let age = 25; // number
let isMarried = false; // boolean
let x; // undefined
let car = null; // null
let symbol = Symbol('symbol'); // symbol
let bigInt = 1234567890123456789012345678901234567890n; // bigint
```

## Object Data Types

Object data types are more complex data types that can be used to store collections of data. There are 3 object data types in Javascript:

- **Object**: a collection of key: value pairs, which can describe data with a more complex structure. Here, the value can be a primitive data type, an array, or even another object. The key is a string that describes the property of the object and is followed by a colon and then the property value.
- **Array**: a collection of values. An array is an object that allows storing multiple values in one variable. An array can contain different data types, including primitive data types, arrays, and objects.
- **Function**: a *block of code* that can be executed by calling it

```javascript
let person = { // object
  firstName: 'John',
  lastName: 'Doe',
  age: 25,
  isMarried: false
};

let fruits = ['apple', 'banana', 'orange']; // array

function sayHello() { // function
  console.log('Hello!');
}
```

## Type Conversion

Type conversion is the process of converting a value from one data type to another. In Javascript, we can convert values from one data type to another using the following methods:

- **String()**: converts a value to a string
- **Number()**: converts a value to a number
- **Boolean()**: converts a value to a boolean

```javascript
let x = 5; // number
let y = String(x); // string - value of y is '5'
let z = Boolean(x); // boolean - value of z is true
```

## Type Coercion

Type coercion is the process of converting a value from one data type to another implicitly. This means that type coercion happens automatically without us having to do it ourselves. In Javascript, type coercion occurs when an operator is used with operands of different data types. For example, the + operator can be used to add two numbers, but it can also be used to concatenate two strings.

```javascript
let x = 5; // number
let y = '5'; // string
let z = x + y; // string - value of z is '55'
```

## Exercises

### Exercise 1

What is the data type of the following variables?

```javascript
let firstName = 'John';
let age = 25;
let isMarried = false;
let x;
let car = null;
```

<details>
<summary>Solution</summary>

- `firstName` is a string
- `age` is a number
- `isMarried` is a boolean
- `x` is undefined
- `car` is null

</details>

### Exercise 2

What is the data type of the following variables?

```javascript
let person = {
  firstName: 'John',
  lastName: 'Doe',
  age: 25,
  isMarried: false
};

let fruits = ['apple', 'banana', 'orange'];

function sayHello() {
  console.log('Hello!');
}
```

<details>
<summary>Solution</summary>

- `person` is an object
  - `firstName`, `lastName`, `age`, and `isMarried` are properties of the `person` object
  - `firstName`, `lastName` are strings
  - `age` is a number
  - `isMarried` is a boolean
- `fruits` is an array
  - `apple`, `banana`, and `orange` are elements of the `fruits` array
  - `apple`, `banana`, and `orange` are strings
- `sayHello` is a function
  - 'Hello!' is a string

</details>
