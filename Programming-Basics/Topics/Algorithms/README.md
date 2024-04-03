# Algorithms

In this topic, we will learn about algorithms and how to design algorithms to solve problems.

- [Algorithms](#algorithms)
  - [Learning Outcomes](#learning-outcomes)
  - [What is an Algorithm?](#what-is-an-algorithm)
  - [Designing Algorithms](#designing-algorithms)
  - [Pseudocode](#pseudocode)
  - [Flowcharts](#flowcharts)
  - [Exercises](#exercises)
    - [Exercise 1](#exercise-1)
    - [Exercise 2](#exercise-2)
    - [Exercise 3](#exercise-3)

## Learning Outcomes

After completing this topic, you'll be able to:

- Define what an algorithm is
- Design simple algorithms
- Write simple algorithms in pseudocode
- Draw simple flowcharts

## What is an Algorithm?

Very often, when we need to solve problem, we tend to jump into writing code without thinking about the problem. This is not a good approach because it can lead to bugs and errors in our code. It is better to first think about the problem and then write code to solve the problem. This is where algorithms come in. 

An algorithm is a specific set of clearly defined instructions or a step-by-step process designed to perform a task or solve a problem. In the context of computer science and programming, algorithms are used to manipulate data, make calculations, process input, and perform automated reasoning or other decision-making processes. Algorithms are used in many different fields, including mathematics, science, engineering, and economics. Actually, we use algorithms in our everyday life, for example, when we follow a recipe to cook a meal, when we follow a set of directions to get to a destination, or when we follow a set of instructions to assemble a piece of furniture.

## Designing Algorithms

When we tryin to solve a problem, then it is a good idea to follow a step-by-step process. This process is called algorithm design. The process of algorithm design involves the following steps:

- Understand the problem
- Identify the inputs and outputs
- Identify the steps needed to solve the problem
- Write the algorithm in pseudocode or draw a flowchart
- Test the algorithm with different inputs
- Refine the algorithm if necessary

## Pseudocode

Pseudocode is a simple, informal language that is used to describe the steps of an algorithm. It is not a programming language, but it is similar to a programming language. It is used to describe the steps of an algorithm in a way that is easy to understand.

For example, the following pseudocode describes the steps of an algorithm that calculates and prints the sum of two numbers:

```
START
    READ number1
    READ number2
    sum = number1 + number2
    PRINT sum
END
```

Since pseudocode is not meant to be executed, it does not have to follow the syntax of a programming language. It is meant to be read by humans, so it should be easy to understand. It is also meant to be written by humans, so it should be easy to write. It is a good idea to use pseudocode when designing algorithms because it allows us to focus on the logic of the algorithm without having to worry about the syntax of a programming language.

However, there are some common conventions often used in pseudocode:

- Basic Control Structures:
  - `IF`...`THEN`...`ELSE` for conditional branches.
  - `FOR`...`DO` for definite loops (loops with a predetermined number of iterations).
  - `WHILE`...`DO` for indefinite loops (loops where the number of iterations is not predetermined).
  - `REPEAT`...`UNTIL` for loops that must execute at least once before the condition is evaluated.

- Variable Assignment and Declaration:
  - Variables are typically declared implicitly when they are first used, and their assignment is often denoted with a simple `=` symbol.

- Input and Output:
  - `READ`, `INPUT`, or similar phrases for taking input.
  - `PRINT`, `DISPLAY`, or similar phrases for outputting results.

- Comments:
  - Often marked with words like `//`, `#`, or `REM`, followed by the comment text, although the specific symbols can vary.

- Subroutines and Functions:
  - Defined with words like `FUNCTION` or `PROCEDURE`, followed by the subroutine name and possibly parameters.
  - `RETURN` is used to indicate the output of the subroutine.

- Array and Data Structure Usage:
  - Arrays or lists might be used without explicit declaration of their size or type.
  - Other data structures like stacks, queues, or trees can be referenced as per their standard operations (e.g., PUSH, POP for stacks).

- Algorithmic Statements:
  - Statements that describe specific actions like `SORT`, `MERGE`, `FIND`, etc.

- Pseudocode Structure:
  - Pseudocode is usually structured and indented to enhance readability.

```
FUNCTION findMax(numbers: LIST OF INTEGER) RETURNS INTEGER
    maxNumber = numbers[0]
    FOR EACH number IN numbers DO
        IF number > maxNumber THEN
            maxNumber = number
        ENDIF
    ENDFOR
    RETURN maxNumber
END FUNCTION
```

This example shows a function in pseudocode to find the maximum number in a list. Notice the use of indentation and simple English terms to make the algorithm clear and understandable

## Flowcharts

A flowchart is a diagram that represents the steps of an algorithm. It is used to describe the steps of an algorithm in a way that is easy to understand. It is a graphical representation of an algorithm that uses symbols to represent the different steps of the algorithm.

For example, the following flowchart describes the steps of an algorithm that calculates and prints the sum of two numbers:

```mermaid
flowchart TD
    A[Start] --> B{{Input number}}
    B --> C{Is number > 0?}
    C -- Yes --> D[Number is positive]
    C -- No --> E{Is number < 0?}
    E -- Yes --> F[Number is negative]
    E -- No --> G[Number is zero]
    D --> H[End]
    F --> H
    G --> H
```
This is a very simple example of a flowchart to describe basic program that checks if a number is positive, negative, or zero.

In flowcharts, the following symbols are used to represent the different steps of an algorithm:

```mermaid
flowchart TD
    A([Start]) -->|leads to| B[Process Step]
    B --> C{Decision?}
    C -->|Yes| D[Output Step]
    C -->|No| E[Another Process]
    D --> F[End]
    E -->|Connects to| G[Subroutine]
    G --> H{{Manual Input}}
    H --> I[Document Generation]
    I --> J[(Database Interaction)]
    J --> F

```

## Exercises

Create a flowchart or write pseudocode for the following algorithms:

### Exercise 1

Write an algorithm that takes two numbers as input and prints the sum of the two numbers.

<details>
<summary>Solution</summary>

```mermaid
flowchart TD
    A[Start] --> B{{Input number1}}
    B --> C{{Input number2}}
    C --> D[sum = number1 + number2]
    D --> E[Print sum]
    E --> F[End]
```
</details>

### Exercise 2

Write an algorithm that takes two numbers as input and prints the larger of the two numbers.

### Exercise 3

Write an algorithm that takes three numbers as input and prints the average of the three numbers.


