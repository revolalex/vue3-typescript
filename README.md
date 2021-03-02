# vue3-typescript
![](https://img.shields.io/badge/made%20with-vue.js-green?logo=vue.js).

## Table of contents
* [Goal](#goal-of-theproject)
* [Creating components](#creating-components-with-typescript)
* [DefineComponent method](#definecomponent-method)
* [Overview of types](#overview-of-types)
* [New type from typescript](#new-types-from-typescript)
* [How to apply a type to a variable](#how-to-apply-a-type-to-a-variable)
* [Array](#arrays)
* [Function](#function)
* [Object](#object)

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







