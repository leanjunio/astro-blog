---
author: Lean Junio
title: Functional Progrmaming Part 1 - Higher-Order Functions
slug: functional-programming-higher-order-functions
tags:
- "Functional Programming"
- "TypeScript"
- "Higher Order Functions"
featured: true
datetime: 2022-11-15T15:43:47.785Z
description: What are higher order functions?
---
In functional programming languages such as JavaScript, functions are also **values**:

```ts
const myFunction = function() {
	console.log('mine');
}
```
An anonymous function was assigned to the `myFunction` variable which makes the anonymous function a
**value** that can be assigned.

We can do that because in functional programming, functions are treated as [first class citizens](https://en.wikipedia.org/wiki/First-class_citizen).
Functions can therefore be passed as arguments to other functions.

Functions that can take functions as arguments are called [Higher-Order Functions](https://en.wikipedia.org/wiki/Functional_programming#First-class_and_higher-order_functions).

#### How is this relevant to JavaScript?

JavaScript is both a functional and an object-oriented language thanks to the developments made
starting in ES6.

This gives us the ability to pass **callback** functions into **higher-order functions** in JavaScript.

A few examples:

```ts
['apple', 'banana', 'orange'].map(fruit => console.log(fruit));

// apple, banana, orange
```

`Array.map` is a higher-order function that allows us to pass an arrow function where our own
logic is defined (logging out the fruit).

Looks simple, but because higher-order functions gives us the ability to build composable code, we can
also utilise the higher-order function to accept a different callback to our own choosing.

```ts
const fruits = ['apple', 'banana', 'orange'];

const addNumbers = (fruit: string, index: number) => `${index + 1}: ${fruit}`;const uppercase = (fruit: string) => `${fruit.toUpperCase()}`;
const includesLetter = (letter: string) => fruit.includes(letter);

fruits.map(addNumbers); 		  // ['1: apple', '2: banana', '3: orange']
fruits.map(uppercase);  		  // ['APPLE', 'BANANA', 'ORANGE']
fruits.map(includesLetter('o'));  // [false, false, true]
```

It is much easier to build on top of pre-existing logic when you're able to utilise
higher-order functions.

In the above example, we were able to create 3 different pieces of logic because `map` can accept
functions as arguments as a higher-order function.

#### How to create higher order functions?

You can create higher order functions the same way that you'd create a normal function. The only
difference is that the higher order function must be able to accept a function as a parameter.

```ts
const enforceValidation = function(validator: Function) {
	const animal = 'dog';
	return validator(animal);
}

const isDog = enforceValidation(animal => animal === 'dog');
const isCat = enforceValidation(animal => animal === 'cat');
const hasLongName = enforceValidation(animal => animal.length > 5);
```