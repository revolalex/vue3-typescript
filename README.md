# vue3-typescript
![](https://img.shields.io/badge/made%20with-vue.js-green?logo=vue.js).

## Table of contents
* [Goal](#goal-of-the-project)
* [Creating components](#creating-components-with-typescript)
* [DefineComponent method](#definecomponent-method)
* [Overview of types](#overview-of-types)
* [New type from typescript](#new-types-from-typescript)
* [How to apply a type to a variable](#how-to-apply-a-type-to-a-variable)
* [Array](#arrays)
* [Function](#function)
* [Object](#object)
* [Defining custom types](#defining-custom-types)
* [What is an interface?](#what-is-an-interface)
* [Lean pratice](#learn-pratice)

## Goal of the project
The goal of this project was to learn to work with typescript and vue3

## Creating Components with TypeScript
One of the most important changes that have happened in our Single File Components (SFC) is that our block now contains a attribute, which stands for language. This is more commonly seen on the block where we declare the use of pre-processors such as Sass.

Given that we want to use TypeScript with our SFCs, this means we also need to configure that on our block by assign the value of to the property.
```js
<script lang="ts">
```
## defineComponent Method
One of the newer things that takes some getting used to in Vue 3 is the importing of helper methods. And while we typically define components in Single File Components (SFC) by writing:

```js
export default { ... }
```
However, when we want to use TypeScript, we need to be explicit with TypeScript that we are declaring JavaScript specific to the SFC. As a result, we have to use a helper method from Vue called .

```js
import { defineComponent } from 'vue'
```
Once we have this, you’ll see that we use it by passing the object we typically export inside of this function:
```js
export default defineComponent({ ... })
```

## Overview of Types
- String
- Number
- Boolean
- Array
- Function
- Object

## New Types from TypeScript
- any - allows you to assign any type to the variable, which is the basic equivalent of disabling type checking
- tuple - allows you to define an array that contains a fixed number of elements with certain types
- enum - allows you to define friendly names to sets of numeric values

## How to Apply a Type to a Variable
```js
let stageName: string = 'A Beautiful Vue'
let roomSize: number = 100
let isComplete: boolean = false
```

## Arrays
In TypeScript, defining arrays is not as straightforward as saying:
```js
let shoppingList: array = ['apple', 'bananas', 'cherries']
```

Because TypeScript is about being more explicit about what types are expected in the array, the notation for defining arrays is a little bit different. Using our shoppingList example from above, we know that the list should only include a strings. As a result, we define the type with:

```js
let shoppingList: string[] = ['apple', 'bananas', 'cherries']
```

## Function
When it comes to adding types to a function, there are a few ways to do this. However, regardless of the methodology, there are two key parts to keep in mind:
- Parameters
- Return

#### Before Typescript
```js
let generateFullName = (firstName, lastName) => {
  return firstName + ' ' + lastName
}
```

#### With Typescript
However, as you might have guessed, this leaves us vulnerable to having random data types being passed into our function when we really only want strings to be passed in. So as a first step, we would define the types expected on our parameters, which in this case are strings.

However, we’re not done yet! The one last thing we need to do is to define what type of data we expect to get from the function, which we do by using the colon (i.e., :) after the parameters.

```js
let generateFullName = (firstName: string, lastName: string): string => {
  return firstName + ' ' + lastName
}
```

## Object

#### Before Typescript
let’s start with the fundamentals of how to define types on object values. In the case of a person object:


```js
let person = {
  name: 'Peter Parker',
  age: 20,
  activeAvenger: true,
  powers: ['wall-crawl', 'spider-sense']
}
```

#### With Typescript
If we wanted to define the types that are expected for each key-value pair in the person object, we define the types through the following syntax:

```js
let person: {
  name: string;
  age: number;
  activeAvenger: boolean;
  powers: string[];
} = {
  name: 'Peter Parker',
  age: 20,
  activeAvenger: true,
  powers: ['wall-crawl', 'spider-sense']
}
```

## Defining Custom Types
As applications grow in size and complexity with unique requirements, it’s inevitable that there will be a need for custom types. 

#### What is types
In its simplest form, type allows you to define an alias that refers to a specific way that the data should be shaped. For example, here were faced with a problem where wanted to confine our buttonStyles variables to certain CSS classes based on a design system.
```js
let buttonStyles: string = 'primary'
```

#### How to use type ?
Similar to declaring a variable, you use type as a declaration of the variable type.

```js
type buttonType = 'primary'
```

In this starting example, we’ve declared a type called buttonType that contains that value 'primary'. And similar to standard type declaration, we can apply this type to our initial example:
```
js let buttonStyles: buttonType = 'primary'
```

As it stands, our buttonStyles is a valid variable because it matches our defined type. At this time, if someone tried to switch the value of buttonStyles to:
```
js let buttonStyles: buttonType = 'secondary'
```

TypeScript would report an error, which is what we expect since buttonType can only be a value of 'primary' at this time. So what if we need multiple values?

### How to define multiple values?
In the event that you need to allow a type to contain multiple values, this is where the union operator comes in. The union operator can be identified by a single pipe | and is most similar to what we’re familiar with in JavaScript as || or in other words, the “OR” operator.

With this knowledge, let’s continue enhancing our buttonType example with the remaining valid button types.
```js 
type buttonType = 'primary' | 'secondary' | 'success' | 'danger'
```

And now when we apply it, we can ensure that all buttonType variables have the correct value!
```js
// TypeScript will report an error because this doesn't exist in the type!
const errorBtnStyles: buttonType = 'error'

// This variable is type safe!
const dangerBtnStyles: buttonType = 'danger'
```

## What is an interface?
When getting started with interface, the way I like to think about it is a way to define a type for an object.

```js
let person: {
	name: string;
	age: number;
	activeAvenger: boolean;
	powers: string[];
} = {
	name: 'Peter Parker',
	age: 20,
	activeAvenger: true,
	powers: ['wall-crawl', 'spider-sense']
}
```

As we can see here, even though the data isn’t too complicated, it’s already fairly verbose and adds clutter to our code. Wouldn’t it be nice if it could look something like this instead?


```js
let person: Hero = {
	name: 'Peter Parker',
	age: 20,
	activeAvenger: true,
	powers: ['wall-crawl', 'spider-sense']
}
```
Well, with an interface, you can totally do this!


#### How to define an interface?
Just like a type, you declare an interface by prefixing the variable name with interface. So using our hero example from above, it would start out looking like this:
```js interface Hero = { } ```

Once we have this structure in place, then it’s only a matter of defining our object types within the interface.

```js
interface Hero {
	name: string;
	age: number;
	activeAvenger: boolean;
	powers: string[];
}
```
And just like that, we can now define variables that will be checked against the type Hero!


#### Can you use type in an interface?
Let’s say we want to enhance our Hero interface by defining what comic-book universe they live in. Well, without the use of type, it might look like this:

```js
interface Hero {
	name: string;
	age: number;
	activeAvenger: boolean;
	powers: string[];
	universe: string;
}
```

But like most applications, this isn’t useful given we want to restrict the universe property to only contain Marvel or DC as a value. Well, it looks like it’s time to call upon our power of type!

```js
type ComicUniverse = 'Marvel' | 'DC'

interface Hero {
	name: string;
	age: number;
	activeAvenger: boolean;
	powers: string[];
	universe: ComicUniverse;
}
```
And just like that, we’ve now combined our interface and type together!

My recommendation for your initial mental model is to use interface for objects, and use type for everything else.

## Learn Pratice
- Overviex of types
- How to add type to variable
- Limitation of predefined types
- How to define custom types
- Use the type and interface type
- Union opérators





