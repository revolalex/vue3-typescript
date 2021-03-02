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
* [What a type assertions?](#what-a-type-assertions)
* [Props with Types](#props-with-types)
* [Custom Types with Computed Properties](#Custom-types-with-computed-properties)
* [Custom Types with Methods](#Custom-types-with-methods)
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

```js 
let buttonStyles: buttonType = 'primary'
```

As it stands, our buttonStyles is a valid variable because it matches our defined type. At this time, if someone tried to switch the value of buttonStyles to:
```js
let buttonStyles: buttonType = 'secondary'
```

TypeScript would report an error, which is what we expect since buttonType can only be a value of 'primary' at this time. So what if we need multiple values?

### How to define multiple values?

In the event that you need to allow a type to contain multiple values, this is where the union operator comes in. The union operator can be identified by a single pipe ```|``` and is most similar to what we’re familiar with in JavaScript as ```||``` or in other words, the “OR” operator.

With this knowledge, let’s continue enhancing our buttonType example with the remaining valid button types.
```js 
type buttonType = 'primary' | 'secondary' | 'success' | 'danger'
```

And now when we apply it, we can ensure that all buttonType variables have the correct value!
```js
// TypeScript will report an error because this doesn't exist in the type!
const errorBtnStyles: buttonType = 'error' ❌

// This variable is type safe!
const dangerBtnStyles: buttonType = 'danger' ✅
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

```js 
interface Hero = { } 
```

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
let person: Hero = {
	name: 'Peter Parker',
	age: 20,
	activeAvenger: true,
	powers: ['wall-crawl', 'spider-sense'],
	universe: 'Marvel'
}
```
And just like that, we’ve now combined our interface and type together!

**My recommendation for your initial mental model is to use interface for objects, and use type for everything else.**

## What are type assertions?
At its core definition, type assertions allow you to override the inferred type by the editor. In other words, it is a way for you to tell the compiler that you know more about the type than it does.

For example, if we have a type called TodoItem and an empty object:
```js
interface TodoItem {
  label: string
  complete: boolean
}

const futureTodoItem = {}

futureTodoItem.label = 'Install VueDX extension'
futureTodoItem.complete = false
```

TypeScript by default, will infer that futureTodoItem is simply an empty object that should not have any properties in it and will report errors stating as such. But we know it should be a TodoItem type, so we can tell TypeScript this by using the as keyword to override the default behavior.

```js
interface TodoItem {
  label: string
  complete: boolean
}

const futureTodoItem = {} as TodoItem

futureTodoItem.label = 'Learn Typescript with vue3'
futureTodoItem.complete = false
```

And just like that, everything works now!

## Props with Types
First we need to see:

#### TypeScript Generics
```js
function createList(item: number): number[] {
    const newList: number[] = []
  
    newList.push(item)
  
    return newList
}

const numberList = createList(123)
```

With this, you get type safety, but the function is rather limiting isn’t it? And if we were to rename it properly, we’d probably want to call it ```addNumberToNumberList```, but this wouldn’t be very reusable then. So the question is, how would we make this more reusable?

In TypeScript, this is solved with the concept of “Generics.” At a high level, they allow you to define a dynamic type that is reused in the function later on. The key marker that generics are being used is when a function is appended with the ```<>``` bracket, which allows you to pass in a type rather than a JavaScript value that is passed in parentheses instead. So the code we had before would become:

```js
function createList<CustomType>(item: CustomType): CustomType[] {
    const newList: CustomType[] = []
  
    newList.push(item)
  
    return newList
}

const numberList = createList<number>(123)
```

You have to know it is a convention in the TypeScript community to use single letter variables — starting with ```T``` — when defining custom types in generics.
So out in other code bases, the same code above would look like this:

```js
function createList<T>(item: T): T[] {
    const newList: T[] = []
  
    newList.push(item)
  
    return newList
}

const stringList = createList<T>(123)
```

#### PropType Helper Method

In Vue 3, when we want to apply custom types to props, we need the built-in helper method called ```PropTypes```. You can use it by importing it from Vue directly.

```js
import { PropTypes } from 'vue'
```

## Custom Types with Computed Properties
Let’s start with computed properties.

EventItem:
```js

export interface EventItem {
  id: number
  category: string
  title: string
  description: string
  location: string
  date: string
  time: string
  organizer: string
}
```


Here we have a standard single file component where the language in the script block is marked for TypeScript.

```js
<script lang="ts">
import { defineComponent } from 'vue'
import { EventItem } from '../types'

export default defineComponent({
  data() {
    return {
      events: []
    }
  },
  methods: {
    secondEvent() {
      return this.events[1]
    }
  }
})
</script>
```

Using what we learned in Data with Custom Types, we know that we can type our events array by using the keyword ```as``` to tell TypeScript that it is an array of ```EventItem```s.

```js
<script lang="ts">
import { defineComponent } from 'vue'
import { EventItem } from '../types'

export default defineComponent({
  data() {
    return {
      events: [] as EventItem
    }
  },
  methods: {
    secondEvent(): EventItem {
      return this.events[1]
    }
  }
})
</script>
```
But what about our computed property?

When it comes to computed properties, the key thing to remember is that you want to focus on what the computed property is returning. In other words, using our example, we need to define what type that ```secondEvent``` will end up returning.

To do this, we use the syntax of the ```:``` and the following it with the custom type the function should return:

```js
<script lang="ts">
import { defineComponent } from 'vue'
import { EventItem } from '../types'

export default defineComponent({
  data() {
    return {
      events: [] as EventItem
    }
  },
  methods: {
    secondEvent(): EventItem {
      return this.events[1]
    }
  }
})
</script>
```

Believe it or not, just like that, you’ve successfully added a custom type to your computed property!

## Custom Types with Methods

Now let’s shift gears to how we add custom types to methods. Let’s start again with our component with a small change where we have an ```addEvent``` method.

```js
<script lang="ts">
import { defineComponent } from 'vue'
import { EventItem } from '../types'

export default defineComponent({
  data() {
    return {
      events: [] as EventItem[]
    }
  },
  methods: {
    addEvent(newEvent) {
      this.events.push(newEvent)
    }
  }
})
</script>
```

In our ```addEvent``` function, we can see that it takes in a parameter of ```newEvent``` and adds it to the events data that we’re tracking inside of ```data()```.

When it comes to adding custom types to methods, there are two key things to keep in mind:

- Do we need to add types to the parameters being passed into the method?
- Do we need to add types to whatever is being returned by the method?

#### Adding Custom Types to the Parameter of a Method
In this particular function, our focus is on add a custom type to the parameter ```newEvent```, which should a type of ```EventItem```. And we can accomplish this by using the ```:``` syntax:

```js
addEvent(newEvent: EventItem) {
  this.events.push(newEvent)
}
```

#### Adding Custom Types to the Return Value of a Method
For this scenario, let’s change up the method to fetching the second event:

```js
secondEvent() {
  return this.events[1]
}
```

If you’re thinking this looks similar to the computed properties example we saw earlier, you’d be correct! The solution to typing your method’s return value is exactly the same.
```js
secondEvent(): EventItem {
  return this.events[1]
}
```
And with that, you know all you need to add custom types to your methods!

If you’re looking for additional resources to explore on your own, be sure to check out:

- The official Vue docs that now has a dedicated TypeScript section that will continue to grow as the ecosystem matures.
https://v3.vuejs.org/guide/typescript-support.html#typescript-support
- And of course, the official TypeScript docs site for an in-depth look at TypeScript
https://www.typescriptlang.org/docs/

## Learn Pratice
- Overview of types
- How to add type to variable
- Limitation of predefined types
- How to define custom types
- What is an interface
- What is a type
- what is union opérators
- what type assertions are
- Use the new 'as' keyword in order to define custom types
- What generics are 
- PropType helper method
- Defining custom types on props
- Custom types with computed properties
- Custom types with methods





