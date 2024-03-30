---
layout: post
title: Is Functional Programming the Way to Go?
subtitle: Exploring Functional Programming from a Junior Developer's Perspective
cover-img: https://images.unsplash.com/photo-1517694712202-14dd9538aa97?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
thumbnail-img:
share-img: https://images.unsplash.com/photo-1517694712202-14dd9538aa97?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
tags: [functional programming, programming paradigms, data pipelines]
author: imsujinpark
---

## Introduction
As someone who first started programming with **JavaScript**, I quickly became accustomed to its methods like `sort`, `filter`, and `map`. I relied on them before truly understanding their underlying principles. Now that I can write logic that achieves the same outcomes without relying on these built-in functions, I find myself pondering the question of which coding approach is truly the most effective. And that's where I began to delve deeper into **functional programming** and other paradigms.

### Which one looks better?
Consider a scenario where you're tasked with filtering a list of groceries, isolating fruits, and then sorting them by price.

```javascript
const groceryList = [
    { name: 'Apple', category: 'fruit', price: 1.25 },
    { name: 'Broccoli', category: 'vegetable', price: 0.75 },
    { name: 'Banana', category: 'fruit', price: 0.5 },
    { name: 'Carrot', category: 'vegetable', price: 1 }
];
```
**Option 1**
```javascript
function filterAndSortFruitsByPrice(groceryList) {
    let fruits = [];

    for (let i = 0; i < groceryList.length; i++) {
        if (groceryList[i].category === 'fruit') {
            fruits.push(groceryList[i]);
        }
    }

    for (let i = 0; i < fruits.length - 1; i++) {
        for (let j = 0; j < fruits.length - i - 1; j++) {
            if (fruits[j].price < fruits[j + 1].price) {
                let temp = fruits[j];
                fruits[j] = fruits[j + 1];
                fruits[j + 1] = temp;
            }
        }
    }
    return fruits;
}
```

**Option 2**
```javascript
const filterAndSortFruitsByPrice = (groceryList) => {
    return groceryList
        .filter(item => item.category === 'fruit')
        .sort((a, b) => b.price - a.price);
};
```
Which one do you think is better?
Well, "better" way of writing code is subjective. But, I think many would agree that the second option is cleaner and easier to read.
It doesn't modify the original array, which leads to fewer side effects and easier debugging.

This is an example of **functional programming**, a coding paradigm that focuses on using functions to process data and avoid changing state or mutable variables.

## Understanding Functional Programming
No State, No Changes in Memory?

**Functional programming, at its core, aims to eliminate state and side effects.**
In simpler terms, it promotes the idea that functions should produce the same output for a given input, without altering state or relying on mutable variables.

This paradigm shift aligns with the **Neumann architecture**, a fundamental concept in computer science. 
This architecture suggests that computers process data by altering states in memory, which traditional imperative programming heavily relies upon. 
However, functional programming challenges this notion by advocating for **statelessness**.

### But Does It Really Have No State?
While it would be ideal for there to be no state and no side effects, this isn't the reality. 

**Computers fundamentally have state**. They store data in memory, and programs manipulate this data to produce results.
Input isn't deterministic, meaning the same input can yield different outputs based on the system's state. And any output necessarily induces side effects by altering the system's state.

Functional programming doesn't mean that there's no state at all.
Rather, it emphasises minimising state and managing it in a controlled manner.
By reducing the reliance on mutable state, functional programming simplifies code, making it easier to reason about and test.

### Lambda Calculus: The Foundation of Functional Programming
Functional programming traces its roots back to **lambda calculus**, a mathematical system developed by Alonzo Church in the 1930s.
It defines computations using anonymous functions, known as lambda functions. These functions treat computation as the evaluation of mathematical functions, emphasising simplicity and universality.

Let's look at the example from earlier, written in a functional style:
```javascript
const filterAndSortFruitsByPrice = (groceryList) => {
    return groceryList
        .filter(item => item.category === 'fruit')
        .sort((a, b) => b.price - a.price);
};
```

`item => item.category === 'fruit'` and `(a, b) => b.price - a.price` are lambda functions. They are not named and are only used where they are defined.

### Making Data Pipelines
**Pipeline** is a series of processing elements, where output of one element is input of the next.

Functional programming encourages the use of **data pipelines**, where data flows through a series of functions, each transforming it in a specific way. This approach promotes composability, allowing developers to combine functions to create complex logic from simple building blocks.

One of the technique for building data pipelines is **currying**. Currying is the process of converting a function that takes multiple arguments into a sequence of functions that each take a single argument. This technique allows for partial application of functions, enabling greater flexibility and reusability.

```javascript
const add = (a) => (b) => a + b; // Curried function which takes one argument `a` and returns a function that takes another argument `b`

const addFive = add(5); // addFive is a function that adds 5 to its argument
console.log(addFive(3)); // Output: 8
```

However, while data pipelines in functional programming offer **flexibility** and **scalability**, it is important to be mindful of its potential bottlenecks and inefficiencies such as excessive function nesting or inefficient data processing.
Thoughtful planning of **how functions are combined** and **how data flows** through the pipeline along with **regular performance testing** can help mitigate these issues.

## What Other Paradigms Are There?
> **Paradigm ?**
> - a way of thinking about something
> - a set of ideas or opinions about how something should be done, made, or thought about

Functional programming is just one of many paradigms in software development.
Other popular paradigms include:

### Imperative Programming
```javascript
let sum = 0;
for (let i = 0; i < 10; i++) {
    sum += i;
}
```
- focuses on how a program operates
- often relies on mutable state and control flow structures like loops and conditionals

#### Procedural Programming
In procedural programming, the code is typically organised into procedures or functions, emphasising the use of functions to perform computations and manage program state.
Below is how the imperative code can be modified to fit into a procedural paradigm:
```javascript
function calculateSum() {
    let sum = 0;
    for (let i = 0; i < 10; i++) {
        sum += i;
    }
    return sum;
}

// Call the function to calculate the sum
let result = calculateSum();
console.log(result);
```

**Imperative Programming** is well-suited for tasks where direct control over program flow and state management are necessary, such as low-level system programming or performance-critical operations where fine-grained control is essential.


### Object Oriented Programming (OOP)
```javascript
class Person {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }

    greet() {
        return `Hello, my name is ${this.name}`;
    }
}
```
- organises code around objects that encapsulate data and behaviour
- encourages code reusability and modularity through concepts like inheritance and polymorphism

**OOP** is particularly effective for modelling real-world entities and relationships like users, products, or transactions, where data and behaviour can be encapsulated within objects. It is particularly useful for large-scale applications with complex data structures and interactions.

## How to Apply Functional Programming in Your Code
Here are some tips to help you apply functional programming principles in your code effectively:
1. Reduce state
    - Minimise reliance on mutable state
    - Use immutable data structures where possible
    - Avoid side effects that alter state outside the function's scope
2. Make data pipelines
    - Create composable functions that transform data
    - Chain functions together to create complex logic
    - Embrace the concept of pure functions that produce the same output for a given input
3. Use lambdas for lightweight generic code
    - Leverage anonymous functions for concise, reusable logic
    - Apply lambda functions to create custom transformations and filters
    - Promote simplicity and universality in code design

## When to Avoid Functional Programming
Functional programming is a powerful paradigm that offers many benefits, but it's not always the best approach for every situation.
Here are some scenarios where functional programming might not be the ideal choice:
1. **Performance-critical applications**
    - Functional programming can introduce overhead due to its emphasis on immutability and statelessness
    - Imperative programming might be more suitable for performance-critical tasks where fine-grained control is essential
2. **Complex state management**
    - Functional programming might not be the best choice for applications with complex state management requirements
    - Object-oriented programming or procedural programming might offer better solutions for managing state and interactions between objects
3. **Legacy codebases**
    - Transitioning a large legacy codebase to a functional programming paradigm can be challenging and time-consuming
    - It might be more practical to maintain the existing codebase using the current paradigm rather than refactoring it entirely

## Conclusion
Function programming offers simplicity and elegance in code design, but it's not always the best approach.
While its focus on statelessness and composability can lead to cleaner, more maintainable code, there are scenarios where mutable state is unavoidable or even beneficial.
**Understanding the underlying principles of functional programming allows us to find the right balance between different paradigms.**

And here is a video that helped me understand functional programming better that made me write this blog post: : [Dear Functional Bros](https://www.youtube.com/watch?v=nuML9SmdbJ4)

Happy coding!