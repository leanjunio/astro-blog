---
author: Lean Junio
title: How to learn JavaScript
slug: how-to-learn-javascript
tags:
- "JavaScript"
- "TypeScript"
- "Nuances"
- "Learning"
featured: true
datetime: 2022-11-15T15:43:47.785Z
description: Just my opinion in terms of how to learn JavaScript
---


These are just some of the tips I wish I knew when I started learning JavaScript

#### 1. [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript ) is your friend

It's very easy to get angry at JavaScript cause it can do these:

![Why](https://res.cloudinary.com/practicaldev/image/fetch/s--Ysm3UtDq--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/4n583bhdqnz03mq3t13v.png)

Understanding how it works is going to be a lot more helpful than going against it.

#### 2. [Understand reference vs primitive types](https://www.freecodecamp.org/news/primitive-vs-reference-data-types-in-javascript/)

The following is possible in JS

```javascript
{} === {} // false
(() => 'hello') === (() => 'hello') // false
new Date() === new Date() // false
```

In JavaScript, objects are a [reference type](https://javascript.info/reference-type).

Storing an object in a variable like so:

```js
const  myObject = {};
```

Does not follow the same process of storing a [primitive type](https://developer.mozilla.org/en-US/docs/Glossary/Primitive) in a variable as such

```js
const number = 4;
```

In the case of the number, the number value is stored in a box that's grouped in a stack of boxes in memory. Retrieving the value is as easy as retrieving the box.

In the case of the object (any reference type really), only the address or location of the value is stored in the box. The computer has to go to the address and actually retrieve the object's value to get it. Therefore, doing `{} === {}` is really just comparing whether the two addresses stored in memory are the same - and the answer is usually no.

#### 3. Understand how [closures](https://medium.com/@samkwon521/eli5-closures-c0018a23e3c5) work

> Closure is when a function is able to remember and access its lexical scope even when the function is executing outside its lexical scope.

```javascript
function outerFunction() {
  let foo = 'foo';

	// has access to the foo variable
  function innerFunction() {
    console.log(foo);
  }

  return innerFunction;
}

// assigned the same address as what's returned from outerFunction()
var basicallyTheInnerFunction = outerFunction();

secondBar(); // foo
```

The string "foo" gets returned here because `secondBar` and `innerFunction` are pointing to the same location in memory.

That piece of memory has access to the lexical context `innerFunction` has which includes the variable `foo`
and its content - the string "foo".

Due to this ability to "access the referential context of a previously executed function (the closure)",
the variable `foo` is not garbage collected until `secondBar` is popped off of the call stack which at that point,
the event loop can go back to doing what's next on its agenda.

