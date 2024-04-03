# Data Structures

In this topic, we'll learn about data structures. We'll learn what a data structure is, what an array is, what an object is, and how to use arrays and objects.

- [Data Structures](#data-structures)
  - [Learning Outcomes](#learning-outcomes)
  - [What is Data Structure?](#what-is-data-structure)
  - [Array](#array)
    - [Array Methods](#array-methods)
      - [Adding Values to an Array](#adding-values-to-an-array)
      - [Finding Values in an Array](#finding-values-in-an-array)
      - [Removing Values from an Array](#removing-values-from-an-array)
    - [Array Iteration](#array-iteration)
  - [Object](#object)
  - [Exercises](#exercises)
    - [Exercise 1 - Basic Array Operations](#exercise-1---basic-array-operations)
    - [Exercise 2 - Array Iteration](#exercise-2---array-iteration)
    - [Exercise 3 - Basic Object Operations](#exercise-3---basic-object-operations)
    - [Exercise 4 - Modifying Object Properties](#exercise-4---modifying-object-properties)

## Learning Outcomes

After completing this topic, you'll be able to:

- Define what a data structure is
- Explain what an array is
- Explain what an object is
- Use arrays and objects
- Use basic array methods

## What is Data Structure?

We already know what variable is and that it is used to store data. But so far we were able to store only one value in a variable or describe only one thing. For example, we could have a variable named `firstName` that stores the first name of a person. But what if we want to store the first name, last name, age, and address of a person? We could create a variable for each of these values, but that would be very inefficient. Instead, we can use a data structure to store all of these values in one place.

A data structure is a way of organizing data in a computer's memory. Data structures are used to store collections of data. For example, we can use an **array** to store a list of numbers or a list of names. We can use an **object** to store information about a person (first name, last name, age, address, etc.). We can use a **set** to store a list of unique values. We can use a **map** to store a list of key-value pairs.

> Even though there are lot of different data structures, we'll focus on arrays and objects in this topic.

## Array

An array is a collection of values that are stored in a single variable. Arrays are used to store lists of values. Arrays are used to store collections of data that are related to each other. For example, we can use an array to store a list of numbers or a list of names.

To create an array, we use the `[]` operator. For example, we can create an array named `numbers` that contains the numbers `1`, `2`, and `3` like this:

```javascript
const numbers = [1, 2, 3];
```
Or we can create an array named `names` that contains the names `John`, `Jane`, and `Jack` like this:

```javascript
const names = ['John', 'Jane', 'Jack'];
```

We can access the values in an array using the index of the value. The index of the first value in an array is `0`. For example, if we want to access the first value in the `numbers` array, we can use the index `0` like this:

```javascript
const numbers = [1, 2, 3];

console.log(numbers[0]);
```
**Expected output**:

```
1
```

We can also use the index of the value to change the value in the array. For example, if we want to change the value of the first value in the `numbers` array to `10`, we can use the index `0` like this:

```javascript
const numbers = [1, 2, 3];

numbers[0] = 10;

console.log(numbers);
```
**Expected output**:

```
[10, 2, 3]
```

### Array Methods

Methods are functions that are associated with an object. It means that in Javascript we can do something with an object by calling a built-in function that is associated with that object.

There are lots of methods that we can use to manipulate arrays. For example, we can use the `push()` method to add a value to the end of an array, the `pop()` method to remove a value from the end of an array, the `shift()` method to remove a value from the beginning of an array, and the `unshift()` method to add a value to the beginning of an array.

All array methods are listed in the [Array Methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) section of the MDN web docs.

#### Adding Values to an Array

We can use the `push()` method to add a value to the end of an array. For example, if we want to add the number `4` to the end of the `numbers` array, we can use the `push()` method like this:

```javascript
const numbers = [1, 2, 3];

numbers.push(4);

console.log(numbers);
```
**Expected output**:

```
[1, 2, 3, 4]
```


#### Finding Values in an Array

We can use the `indexOf()` method to find the index of a value in an array. For example, if we want to find the index of the number `2` in the `numbers` array, we can use the `indexOf()` method like this:

```javascript
const numbers = [1, 2, 3];

console.log(numbers.indexOf(2));
```
**Expected output**:

```
1
```

> If the value is not found in the array, the `indexOf()` method will return `-1`.

#### Removing Values from an Array

We can use splice() method to remove a value from an array. For example, if we want to remove the number `2` from the `numbers` array, we can use the `splice()` method like this:

```javascript
const numbers = [1, 2, 3];

numbers.splice(1, 1);

console.log(numbers);
```
**Expected output**:

```
[1, 3]
```

> The first argument of the `splice()` method is the index of the value that we want to remove and the second argument is the number of values that we want to remove.
> The `splice()` method will return an array of the removed values.
> If we don't specify the second argument, the `splice()` method will remove all values starting from the index that we specified in the first argument.
> If we specify the second argument as `0`, the `splice()` method will not remove any values.
> Remember, that to remove a value from array using this method, we need to know the index of the value that we want to remove.

### Array Iteration

We can use the `for` loop to iterate over an array. For example, if we want to print each value in the `numbers` array on a new line, we can use the `for` loop like this:

```javascript
const days = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday'];

for (let i = 0; i < numbers.length; i++) {
  console.log(numbers[i]);
}
```
**Expected output**:

```
Monday
Tuesday
Wednesday
Thursday
Friday
Saturday
Sunday
```

> Pay attention to the condition of the `for` loop. We need to use the `length` property of the array in the condition of the `for` loop to make sure that we don't go out of bounds of the array.
> 
> The `length` property of an array returns the number of values in the array.
> 
> The `length` property of an array is always one more than the index of the last value in the array.
> 
> Also, remember, that `i` is the value, that increments on each iteration of the `for` loop. We can use the value of `i` to access the values in the array.
> 
> Index of the first value in an array is `0`, so the index of the last value in an array is `length - 1`.

## Object

An object is a collection of key-value pairs that are stored in a single variable. Objects are used to store information about something. For example, we can use an object to store information about a person (first name, last name, age, address, etc.).

To create an object, we use the `{}` operator. For example, we can create an object named `person` that contains the first name `John`, the last name `Doe`, and the age `25` like this:

```javascript
const person = {
  firstName: 'John',
  lastName: 'Doe',
  age: 25
};
```

We can access the values in an object using the key of the value. For example, if we want to access the first name in the `person` object, we can use the key `firstName` like this:

```javascript
const person = {
  firstName: 'John',
  lastName: 'Doe',
  age: 25
};

console.log(person.firstName); // John
```

We can also use the key of the value to change the value in the object. For example, if we want to change the value of the first name in the `person` object to `Jane`, we can use the key `firstName` like this:

```javascript
const person = {
  firstName: 'John',
  lastName: 'Doe',
  age: 25
};

person.firstName = 'Jane';

console.log(person); // { firstName: 'Jane', lastName: 'Doe', age: 25 }
```

As for arrays, there are lots of methods that we can use to manipulate objects also. For example, we can use the `Object.keys()` method to get an array of the keys in an object, the `Object.values()` method to get an array of the values in an object, and the `Object.entries()` method to get an array of the key-value pairs in an object.

All object methods are listed in the [Object Methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object) section of the MDN web docs.

## Exercises

Create a file named `index.js` (or another name of your choice) and start adding solutions to the exercises below.

> Always test your code by running the `index.js` file using the `node index.js` command.

### Exercise 1 - Basic Array Operations

**Objective**: Add elements to an array and print them.

**Description**: Create an array to store a list of three favorite fruits. Add two more fruits to the array using array methods. Finally, print each fruit in the array on a new line.

> You can use the `push()` method to add elements to an array.
> 
> Use the `for` loop to print each element in the array on a new line.

<details>
  <summary>Solution</summary>

```javascript
const fruits = ['apple', 'banana', 'orange'];

fruits.push('strawberry');
fruits.push('pineapple');

for (let i = 0; i < fruits.length; i++) {
  console.log(fruits[i]);
}
```
![Array](array.gif)

</details>

### Exercise 2 - Array Iteration

**Objective**: Find the sum of all numbers in an array.

**Description**: Write a JavaScript program that creates an array of numbers. Iterate over the array and compute the sum of its elements. Print the final sum.

> Probably You need to use extra variable to store the sum of all numbers.

<details>
  <summary>Solution</summary>

```javascript
const numbers = [1, 2, 3, 4, 5];

let sum = 0;

for (let i = 0; i < numbers.length; i++) {
  sum += numbers[i];
}

console.log(sum);
```
**Expected output**:

```
15
```
</details>

### Exercise 3 - Basic Object Operations

**Objective**: Create an object and access its properties.

**Description**: Define a JavaScript object named `car` with properties `make`, `model`, and `year`. Assign appropriate values to each. Then, print the `make` and `year` of the car in a sentence.

> You can access the properties of an object using the `.` operator.
>
> You can use the `+` operator to concatenate strings or use template literals.

<details>
  <summary>Solution</summary>

```javascript
const car = {
  make: 'Toyota',
  model: 'Corolla',
  year: 2019
};

console.log(`I drive a ${car.year} ${car.make} ${car.model}.`);
```

**Expected output**:

```
I drive a 2019 Toyota Corolla.
```
![Object](object.gif)

</details>

### Exercise 4 - Modifying Object Properties

**Objective**: Update and add new properties to an object.

**Description**: Given an object `student` with properties `name`, `age`, and `grade`, update the `age`, add a new property `subject`, and then print the entire object.

Example `student` object:

```javascript
const student = {
  name: 'John Doe',
  age: 16,
  grade: 10
};
```

> You can update the properties of an object using the `.` operator.
>
> You can add new properties to an object using the `.` operator.
>
> You can use `console.log()` to print the entire object.

<details>
  <summary>Solution</summary>

```javascript
const student = {
  name: 'John Doe',
  age: 16,
  grade: 10
};

student.age = 17;

student.subject = 'Math';

console.log(student);
```

**Expected output**:

```
{ name: 'John Doe', age: 17, grade: 10, subject: 'Math' }
```

</details>