# Operators and Expressions

In this topic, we'll learn about operators and expressions in Javascript.

- [Operators and Expressions](#operators-and-expressions)
  - [Learning Outcomes](#learning-outcomes)
  - [What is an Operator?](#what-is-an-operator)
  - [What is an Expression?](#what-is-an-expression)
  - [Relationship between Operators and Expressions:](#relationship-between-operators-and-expressions)
  - [Operator Types](#operator-types)
    - [Arithmetic Operators](#arithmetic-operators)
    - [Assignment Operators](#assignment-operators)
    - [Comparison Operators](#comparison-operators)
    - [Logical Operators](#logical-operators)
    - [Bitwise Operators (optional - not used during the course)](#bitwise-operators-optional---not-used-during-the-course)
    - [String Operators](#string-operators)
    - [Conditional (Ternary) Operator](#conditional-ternary-operator)
    - [Comma Operator](#comma-operator)
    - [Unary Operators](#unary-operators)
    - [Relational Operators](#relational-operators)
  - [Exercises](#exercises)
    - [Exercise 1 -  Basic Arithmetic Operators](#exercise-1----basic-arithmetic-operators)
    - [Exercise 2 -  Comparison Operators](#exercise-2----comparison-operators)
    - [Exercise 3: Logical Operators and Conditional Statements](#exercise-3-logical-operators-and-conditional-statements)

## Learning Outcomes

After completing this topic, you'll be able to:

- Define what an operator is
- Define what an expression is
- Differentiate between operators and expressions
- List the most common operators in Javascript
- Explain the difference between the different types of operators
- Use operators in your programs
- Explain the difference between the equality operator (`==`) and the strict equality operator (`===`)
- Explain the difference between the inequality operator (`!=`) and the strict inequality operator (`!==`)

## What is an Operator?

An operator is a symbol that is used to perform an operation on one or more values. For example, the `+` symbol is used to add two values together. The values that an operator operates on are called operands. For example, in the expression `5 + 10`, the `+` symbol is the operator and `5` and `10` are the operands.

```javascript
let x = 5 + 10; // 5 and 10 are operands, + is the operator. x is the variable that stores the result of the operation
```

## What is an Expression?

An expression is a combination of values, variables, operators, and functions that are evaluated to produce a result. For example, `2 + 3` is an expression that evaluates to `5`. Expressions can be used to perform calculations, manipulate strings, and more.

## Relationship between Operators and Expressions:

- The primary relationship is that operators are used within expressions to define the kind of operation being performed on the operands. An expression might consist of a simple operation with only one operator (like x + y) or a more complex operation with multiple operators (like (x + y) * (a - b)).
- The type of the operator dictates the type of the expression. For instance, arithmetic operators create arithmetic expressions, logical operators create logical expressions, and so on.
- The evaluation of expressions often follows a specific order of operations, determined by the precedence and associativity of the operators involved.

## Operator Types

There are many different types of operators in Javascript. We'll cover the most common ones in this topic.

### Arithmetic Operators

Arithmetic operators are used to perform arithmetic operations on numeric values. We need arithmetic operators when we want to do calculations in our programs. For example, we might want to add two numbers together or multiply two numbers together.

There are 5 arithmetic operators in Javascript:

- `+`: addition - adds two values together
- `-`: subtraction - subtracts one value from another
- `*`: multiplication - multiplies two values together
- `/`: division - divides one value by another
- `%`: modulus - returns the remainder of dividing one value by another

```javascript
let x = 5 + 10; // addition - result is 15
let y = 5 - 10; // subtraction - result is -5
let z = 5 * 10; // multiplication - result is 50
let w = 5 / 10; // division - result is 0.5
let v = 5 % 10; // modulus - result is 5
```

### Assignment Operators

Assignment operators are used to assign values to variables. Sometimes we want to assign a value to a variable and then perform an operation on the variable. For example, we might want to add 10 to a variable and then assign the result to the variable.
There are 8 assignment operators in Javascript:

- `=`: assigns a value to a variable
- `+=`: adds a value to a variable and assigns the result to the variable
- `-=`: subtracts a value from a variable and assigns the result to the variable
- `*=`: multiplies a variable by a value and assigns the result to the variable
- `/=`: divides a variable by a value and assigns the result to the variable
- `%=`: divides a variable by a value and assigns the remainder to the variable
- `**=`: raises a variable to the power of a value and assigns the result to the variable
- `++`: increments a variable by 1
- `--`: decrements a variable by 1

```javascript
let x = 5; // declares variable x and assigns the value 5 to x
x += 10; // adds 10 to x and assigns the result to x - result is 15
x -= 10; // subtracts 10 from x and assigns the result to x - result is 5
x *= 10; // multiplies x by 10 and assigns the result to x - result is 50
x /= 10; // divides x by 10 and assigns the result to x - result is 5
x %= 10; // divides x by 10 and assigns the remainder to x - result is 5
x **= 2; // raises x to the power of 2 and assigns the result to x - result is 25
x++; // increments x by 1 - result is 26
x--; // decrements x by 1 - result is 25
```

### Comparison Operators

Comparison operators are used to compare two values. Comparing values is useful when we want to check if two values are equal or not, or if one value is greater than or less than another value. Result of a comparison is a boolean value (`true` or `false`).
There are 8 comparison operators in Javascript:

- `==`: equal to - returns `true` if two values are equal
- `!=`: not equal to - returns `true` if two values are not equal
- `>`: greater than - returns `true` if the first value is greater than the second value
- `<`: less than - returns `true` if the first value is less than the second value
- `>=`: greater than or equal to - returns `true` if the first value is greater than or equal to the second value
- `<=`: less than or equal to - returns `true` if the first value is less than or equal to the second value
- `===`: strict equal to - returns `true` if two values are equal and of the same type
- `!==`: strict not equal to - returns `true` if two values are not equal or not of the same type

```javascript
let x = 5;
let y = 10;
let z = '5';

x == y; // false
x != y; // true
x > y; // false
x < y; // true
x >= y; // false
x <= y; // true
x === y; // false
x !== y; // true
x == z; // true
x === z; // false
```

> We should always use strict equality (`===`) and strict inequality (`!==`) when comparing values, because as we can see in the example above, the equality operator (`==`) and the inequality operator (`!=`) can produce unexpected results.
>
> For example, `5 == '5'` returns `true`, but `5 === '5'` returns `false`. This is because the equality operator (`==`) converts the operands to the same type before comparing them, but the strict equality operator (`===`) does not convert the operands to the same type before comparing them.

### Logical Operators

Logical operators are used to combine two or more boolean values and return a single boolean value. For example, we might want to check if a number is greater than 10 and less than 20. We can do this by combining two comparison operators using the logical AND operator (`&&`).

There are 3 logical operators in Javascript:

- `&&`: logical AND - returns `true` if both operands are `true`
- `||`: logical OR - returns `true` if one of the operands is `true`
- `!`: logical NOT - returns `true` if the operand is `false`

```javascript
let x = 5;
let y = 10;

x > 5 && x < 10; // false
x > 5 || x < 10; // true
!(x > 5); // true
```

### Bitwise Operators (optional - not used during the course)

Bitwise operators are used to perform bitwise operations on numeric values. Bitwise operations are operations that are performed on the binary representation of a number. For example, the binary representation of the number `5` is `101`. The binary representation of the number `10` is `1010`. The bitwise AND operation on the numbers `5` and `10` is `0`, because `101` AND `1010` is `0`. Counting from right to left, the first bit of the result is `0` because the first bits of the operands are `1` and `0`. The second bit of the result is `0` because the second bits of the operands are `0` and `1`. The third bit of the result is `0` because the third bits of the operands are `1` and `0`.

There are 7 bitwise operators in Javascript:

- `&`: bitwise AND - returns `1` if both bits are `1`
- `|`: bitwise OR - returns `1` if one of the bits is `1`
- `^`: bitwise XOR - returns `1` if one of the bits is `1` and the other is `0`
- `~`: bitwise NOT - flips the bits
- `<<`: bitwise left shift - shifts the bits to the left
- `>>`: bitwise right shift - shifts the bits to the right
- `>>>`: bitwise unsigned right shift - shifts the bits to the right and fills the empty bits with `0`

```javascript
let x = 5; // 101
let y = 10; // 1010

x & y; // 0 - 101 AND 1010 is 0
x | y; // 15 - 101 OR 1010 is 1111
x ^ y; // 15 - 101 XOR 1010 is 1111
~x; // -6 - flips the bits of 101 to get 010 and then converts 010 to decimal to get -6
x << 1; // 10 - shifts the bits of 101 to the left by 1 to get 1010
x >> 1; // 2 - shifts the bits of 101 to the right by 1 to get 10
x >>> 1; // 2 - shifts the bits of 101 to the right by 1 to get 10 and fills the empty bit with 0
```

### String Operators

String operators are used to concatenate strings together. For example, we might want to concatenate the first name and last name of a person to get their full name.

There is only one string operator in Javascript:

- `+`: concatenation - concatenates two strings together

```javascript
let firstName = 'John';
let lastName = 'Doe';

firstName + ' ' + lastName; // 'John Doe'
```

### Conditional (Ternary) Operator

The conditional operator is used to assign a value to a variable based on a condition. For example, we might want to assign a value of `true` to a variable if a number is greater than 10, or a value of `false` if a number is less than 10.

There is only one conditional operator in Javascript:

- `?:`: conditional - assigns a value to a variable based on a condition

```javascript
let x = 5;

x > 10 ? true : false; // false
```

### Comma Operator

The comma operator is used to evaluate multiple expressions and return the result of the last expression. For example, we might want to evaluate two expressions and return the result of the second expression.

There is only one comma operator in Javascript:

- `,`: comma - evaluates multiple expressions and returns the result of the last expression

```javascript
let x = 5;

(x = 10, x + 5); // 15
```

### Unary Operators

Unary operators are used to perform unary operations on a single value. For example, we might want to increment a number by 1 or decrement a number by 1.

There are 3 unary operators in Javascript:

- `+`: unary plus - converts a value to a number
- `-`: unary minus - converts a value to a number and negates it
- `!`: logical NOT - returns `true` if the operand is `false`

```javascript
let x = '5';

+x; // 5
-x; // -5
!x; // false
```

### Relational Operators

Relational operators are used to compare two values. For example, we might want to check if a number is greater than 10 or less than 10.

There are 2 relational operators in Javascript:

- `in`: returns `true` if a property exists in an object
- `instanceof`: returns `true` if an object is an instance of a class

```javascript
let person = {
  firstName: 'John',
  lastName: 'Doe',
  age: 25,
  isMarried: false
};

'firstName' in person; // true
'fullName' in person; // false
person instanceof Object; // true
```

## Exercises

Create a file `index.js` and write the code for the following exercises in this file.

Test your code by running the `index.js` file using the `node index.js` command.

Also, test your code with different values for the variables.

### Exercise 1 -  Basic Arithmetic Operators

**Objective**: Perform basic arithmetic operations.

**Description**: Write a program that declares two variables, `num1` and `num2`, assigned with numbers. Perform addition, subtraction, multiplication, and division on these variables. Print the results of each operation.

**Expected output**: The sum, difference, product, and quotient of `num1` and `num2`.

<details>
  <summary>Solution</summary>

  ```javascript
  let num1 = 5;
  let num2 = 10;

  console.log(num1 + num2); // 15
  console.log(num1 - num2); // -5
  console.log(num1 * num2); // 50
  console.log(num1 / num2); // 0.5
  ```
![Operators](operators.gif)

</details>

### Exercise 2 -  Comparison Operators
**Objective**: Compare two values using different comparison operators.

**Description**: Define two variables with numeric values. Use comparison operators (`==`, `!=`, `>`, `<`, `>=`, `<=`) to compare these values, and print the results of each comparison in a descriptive way.

**Expected output**: Statements indicating the result of each comparison between `a` and `b`.

<details>
  <summary>Solution</summary>

  ```javascript
  let a = 5;
  let b = 10;

  console.log(a == b); // false
  console.log(a != b); // true
  console.log(a > b); // false
  console.log(a < b); // true
  console.log(a >= b); // false
  console.log(a <= b); // true
  ```
</details>

### Exercise 3: Logical Operators and Conditional Statements

**Objective**: Make decisions using logical operators.

**Description**: Write a program that declares three variables `age`, `license`, and `goodVision`. Using logical operators (`&&`, `||`, `!`), determine if a person is eligible to drive a car. The criteria for eligibility are: age must be 18 or over, must have a driving license, and must have good vision.

> Hint: To make a decision, we can use the `if` statement.
>
> `&&` is the logical AND operator. It returns `true` if both operands are `true`.
>
> `||` is the logical OR operator. It returns `true` if one of the operands is `true`.
>
> `!` is the logical NOT operator. It returns `true` if the operand is `false`.

**Example Code**:
```javascript
let age = 25;
let license = true;
let goodVision = true;

// Determine eligibility to drive and print the result
```

**Expected output**: A statement indicating whether the person meets the driving eligibility criteria.
