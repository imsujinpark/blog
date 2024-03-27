---
layout: post
title: What is Hoisting?
subtitle: Understanding the JavaScript mechanism where variables and function declarations are moved to the top of their scope before code execution
cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/thumb.png
share-img: /assets/img/path.jpg
tags: [JavaScript, Hoisting]
author: imsujinpark
---

# Hoisting

## What is Hoisting?
- Hoisting is a JavaScript mechanism where variables and function declarations are moved to the top of their scope before code execution.
- This process is done by the JavaScript engine during the compilation phase.
    - compilation phase: The JavaScript engine scans the code and sets up memory space for variables and functions.
- This means that no matter where functions and variables are declared, they are moved to the top of their scope regardless of whether their scope is global or local.

## Variable Hoisting Example
```javascript
console.log(x); // undefined
var x = 5;
console.log(x); // 5
```
It does not throw an error because the variable declaration is hoisted to the top of the scope.

### Does it only work with `var`?
- No, it also works with `let` and `const`.

## Function Hoisting Example
```javascript
foo(); // "Hello, World!"
function foo() {
    console.log("Hello, World!");
}
```

```javascript
bar(); // Uncaught ReferenceError: Cannot access 'bar' before initialization
const bar = () => {
    console.log("Hello, World!");
}
```
Function declarations are hoisted to the top of their scope, but function expressions are not hoisted.

### Different Types of Function Declarations
1. Function Declaration
```javascript
function foo() {
    console.log("Hello, World!");
}
```
2. Function Expression
```javascript
const bar = function() {
    console.log("Hello, World!");
}
```
3. Arrow Function Expression
```javascript
const baz = () => {
    console.log("Hello, World!");
}
```
| Function Type | Pros | Cons | Hoisted? |
| --- | --- | --- | --- |
| Function Declaration | - Can be called before the declaration<br>- More readable | - Can only be used in the global scope<br>- Can't be assigned to a variable | Yes |
| Function Expression | - Can be assigned to a variable<br>- Can be used in the local scope | - Can't be called before the declaration | No |
| Arrow Function Expression | - Shorter syntax<br>- No `this` binding | - Can't be used in the global scope | No |

## Pros and Cons of Hoisting
### Pros
- It allows you to use functions before they are declared.
- It makes the code more readable by moving all the declarations to the top of the scope.
- It helps avoid `ReferenceError` by hoisting the variable declarations.
### Cons
- It can be confusing if you are not familiar with the hoisting mechanism.
- It can lead to bugs if you rely on hoisting too much.
- It can make the code harder to read and understand if you have a lot of hoisted declarations.

## Conclusion
- Hoisting is a JavaScript mechanism where variables and function declarations are moved to the top of their scope before code execution.
- It works with `var`, `let`, and `const` declarations.
- Function declarations are hoisted, but function expressions are not.
- Hoisting can be useful for using functions before they are declared, but it can also lead to confusion and bugs if not used properly.
