# Vue Workshop

This guide explains how to work with Typescript single file components, using class syntax.
- Class syntax makes a vue component much easier to read
- Typescript provides live error checking while typing in your IDE
Please note that this syntax is different from the default Javascript syntax that is used in the [Vue Getting Started documentation](https://vuejs.org/v2/guide/)

## Contents

- Installing
- Vue Workflow
- What is a Vue component
- Single file components
- Class syntax
- Reactive data
- Adding Props
- Adding Events
- Reading list and documentation

## Installing

Follow the [installation instructions](https://github.com/HR-CMGT/vue-starter)

## Vue Workflow

Study the [Vue Workflow presentation](workflow.md)

## What is a Vue component

A Vue component is a DOM element that can have data and interactivity. A Vue component can respond very fast to changes in the state of your app. When you declare a Vue component, you can add:

- **data**: data contains the state of your component. For example: `user = "erik"`
- **methods**: actions that your component can execute, for example: `loadStarWarsData()`
- **lifecycle**: Each Vue component has a number of default methods, called [lifecycle hooks](https://vuejs.org/v2/guide/instance.html).  

As we have seen in the presentation, a component can have child components, creating a hierarchy. Child components can have:

- **props**: information that the component receives from a parent component
- **events**: information that the component broadcasts to parent components

## Single file components

A `.vue` file contains HTML, CSS and Code for one single component. This makes components easily reusable and prevents spaghetti code.
```
<template>
   <div>Hello world</div>
</template>

<script>
   // our vue component code goes here
</script>

<css>
   div {border: 1px solid black;}
</css>
```
When compiling, webpack extracts these .vue files into separate script and css files, but we don't need to worry about that!

## Class syntax

In this tutorial, we use class syntax to define our Vue components. HR CMGT PRG06 students are already familiar with this syntax since we used it to build [games in Typescript](https://github.com/HR-CMGT/Typescript).

In Vue, we can create a component by extending (inheriting) the default Vue class. Data is defined as properties of the class. This example has a `name` as `data`, a custom method and a lifecycle method:

```
<script lang="ts">
import { Vue, Component } from "vue-property-decorator";

@Component
export default class App extends Vue {
    name: string = "world!"
    sayHello() {
        console.log("hello " + this.name)
    }
    created(){
        console.log("this vue component was just created!")
    }
}
</script>
```

## Reactive data

So far, we could have done all this with regular Typescript. The strength of Vue is that it we can bind our interface elements directly to the data in our components. This is called **reactive data**. 

To connect the data of our component to our DOM elements, we use moustache syntax: `<div>{{ variable }}</div>`. Let's build a single file component with reactive data. In the `created` method, we change the name over time. You will see that the DOM element automatically changes along.

We no longer need to access the DOM manually by using `element = document.getElementById()` and `element.innerHTML = name`!
```
<template>
   <div>Hello {{ name }}</div>
</template>

<script lang="ts">
import { Vue, Component } from "vue-property-decorator";

@Component
export default class App extends Vue {
    name: string = "world"
    created(){
        setInterval(()=>this.updateName(), 500)
    }
    updateName(){
        this.name += "!"
    }
}
</script>
```

## But does it run?

Run `webpack` in your terminal and open the page in localhost. For debugging, open the Vue inspector in Chrome.

## Adding Props

## Adding Events

## Reading List

- [Vue documentation: Introduction](https://vuejs.org/v2/guide/index.html)
- [Vue documentation: Single File Components](https://vuejs.org/v2/guide/single-file-components.html)
- [CSS Tricks: introduction to Vue](https://css-tricks.com/intro-to-vue-1-rendering-directives-events/)
- [Typescript Class Components tutorial](https://alligator.io/vuejs/typescript-class-components/)
- [Vue Class Component on github](https://github.com/vuejs/vue-class-component)
- [Vue documentation: typescript support](https://vuejs.org/v2/guide/typescript.html)
- [Using Vue components without Webpack](https://vuejsdevelopers.com/2017/09/24/vue-js-single-file-javascript-components/)
- [Microsoft Typescript Vue Starter](https://github.com/Microsoft/TypeScript-Vue-Starter)
- [Previous Typescript examples HR CMGT](https://github.com/HR-CMGT/Typescript)
