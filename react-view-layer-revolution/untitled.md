# React Syntax

## React Stack

React V16.8, Redux, Redux-saga, styled-component/Material UI, Navigation: React-router, Forms: React-Hook-Form, axios, Node.js/Next.js/Nuxt.js

## What is Imperative Implementation and Declarative Programming mean?

### Imperative Implementation

It is basically telling the computer **how** to do something, and as a result what you want to happen will happen.

### Declarative Programming

In declarative programming, the program tells the computer **what** you would like to happen, and lets the computer figure out how to do it.

### Perspective in React

The React component never actually touches an element. it simply declares an element _should_ be rendered given our current state. It does not actually manipulate the DOM itself.

When writing React, it’s often good not to think of _how_ you want to accomplish a result, but instead _what_ the component should look like in its new state.This sets us up for a good control flow where state goes through a series of predictable and replicable mutations. This doesn’t just apply to components either, but also to application state. Libraries like [Redux](http://redux.js.org/) will help enforce this method of architecting, but they aren’t necessary to achieve it.

## How React works? How Virtual-DOM works in React?

### React work principles

React creates a virtual DOM. When state changes in a component it firstly runs a “diffing” algorithm, which identifies what has changed in the virtual DOM. The second step is reconciliation, where it updates the DOM with the results of diff.

The HTML DOM is always tree-structured — which is allowed by the structure of HTML document. The DOM trees are huge nowadays because of large apps. Since we are more and more pushed towards dynamic web apps (Single Page Applications — SPAs), we need to modify the DOM tree incessantly and a lot. And this is a real performance and development pain.

### Virtual-DOM work principles

The Virtual DOM is an abstraction of the HTML DOM. It is lightweight and detached from the browser-specific implementation details. It is not invented by React but it uses it and provides it for free. `ReactElements` lives in the virtual DOM. They make the basic nodes here. Once we defined the elements, `ReactElements` can be render into the "real" DOM.

Whenever a `ReactComponent` is changing the state, diff algorithm in React runs and identifies what has changed. And then it updates the DOM with the results of diff. The point is - it’s done faster than it would be in the regular DOM.

## How Virtual-DOM is more efficient than Dirty checking?

In React, each of our components have a state. This state is like an observable. Essentially, React knows when to re-render the scene because it is able to observe when this data changes. Dirty checking is slower than observables because we must poll the data at a regular interval and check all of the values in the data structure recursively. By comparison, setting a value on the state will signal to a listener that some state has changed, so React can simply listen for change events on the state and queue up re-rendering.

The virtual DOM is used for efficient re-rendering of the DOM. This isn’t really related to dirty checking your data. We could re-render using a virtual DOM with or without dirty checking. In fact, the diff algorithm is a dirty checker itself.

We aim to re-render the virtual tree only when the state changes. So using an observable to check if the state has changed is an efficient way to prevent unnecessary re-renders, which would cause lots of unnecessary tree diffs. If nothing has changed, we do nothing.

## What is JSX? Can browser recognize the JSX? Why?

### **Definition**

**JSX is a syntax extension to JavaScript and comes with the full power of JavaScript.**&#x20;

JSX produces React “elements”. You can embed any JavaScript expression in JSX by wrapping it in curly braces. After compilation, JSX expressions become regular JavaScript objects. This means that you can use JSX inside of if statements and for loops, assign it to variables, accept it as arguments, and return it from functions. Even though React does not require JSX, it is the recommended way of describing our UI in React app.

### JSX with Browser

JSX is not valid JavaScript, web browsers cant read it directly. So, if JavaScript files contains JSX, that that file will have to be transpiled. That means that before the file gets to the web browser, a JSX compiler will translate any JSX into regular JavaScript.

JSX produces React “elements”. A React element is simply an object representation of a DOM node. A React element isn’t actually the thing we see on our screen, instead, it’s just an object representation of it. We can embed any JavaScript expression in JSX by wrapping it in curly braces.\


## What is the difference between state and props?

### State

State is a way for a component to store an internal state and it is perfect for when you need to store a field value or perhaps toggle a modal.

### **Props**

Props is what is being passed to the component from the parent element and immutable as far as the Component receiving them is concerned, this is how you most commonly work with data in React.

### Difference

Props and State do similar things but are used in different ways. The majority of our components will probably be stateless. Props are used to pass data from parent to child or by the component itself. They are immutable and thus will not be changed. State is used for mutable data, or data that will change. This is particularly useful for user input.

## What is the context in React?

Context provides a way to pass data through the component tree without having to pass props down manually at every level.

Sometimes we have to pass the props down the component tree even though all the middle components don’t need those. Context is a way to pass the props without passing down the component tree on every level.

{% embed url="https://reactjs.org/docs/context.html" %}

## What is the lifting state up?

In React, sharing state is accomplished by moving it up to the closest common ancestor of the components that need it. This is called “lifting state up”.

Often, several components need to reflect the same changing data. We recommend lifting the shared state up to their closest common ancestor.

## How to Update State and How to avoid the wrong way?

You should not modify the state directly. The only place you can assign to the state is in the constructor. Using the state directly doesn’t trigger the re-rendering. React merges the state when we use `this.setState().`

```jsx
//  wrong way
this.state.name = "some name"

// right way
this.setState({name:"some name"})
```

It’s always safe to use the second form of `this.setState()` because props and state updated are asynchronous. Here we are updating the state based on the props.

```jsx
// wrong way
this.setState({
    timesVisited: this.state.timesVisited + this.props.count
});

// right way
this.setState((state, props) => {
    timesVisited: state.timesVisited + props.count
});
```

## Is setState() is async? If yes, why is setState() in React Async instead of Sync?

`setState()` actions are asynchronous and are batched for performance gains. This is explained in documentation as below.

`setState()` does not immediately mutate this.state but creates a pending state transition. Accessing this.state after calling this method can potentially return the existing value. There is no guarantee of synchronous operation of calls to setState and calls may be batched for performance gains.

This is because setState alters the state and causes rerendering. This can be an expensive operation and making it synchronous might leave the browser unresponsive. Thus the setState calls are asynchronous as well as batched for better UI experience and performance.

## What is the second argument that can optionally be passed to setState and what is its purpose?

A callback function which will be invoked when `setState` has finished and the component is re-rendered.

Since the `setState` is asynchronous, which is why it takes in a second callback function. With this function, we can do what we want immediately after state has been updated.

## If I want to pass some certain data into the event handler, how would you do?

#### Example 1

```jsx
handleEvent = e => {
	this.setState({
		state: e.target.value
	});
}

...

(<input
	placeholder={...}
	onChange={this.handleEvent}
	value={...}
/>)
```

#### Example 2

```jsx
...

(<input
	placeholder={...}
	onChange={this.handleEvent.bind(this)}
	value={...}
/>)
```

## What is the HOC? Why do we need this in the react?

A higher-order component (HOC) is an advanced technique in React for reusing component logic. HOCs are not part of the React API. They are a pattern that emerges from React’s compositional nature.

A higher-order component is a function that takes a component and returns a new component.

HOC’s allow you to reuse code, logic and bootstrap abstraction. HOCs are common in third-party React libraries. The most common is probably Redux’s connect function. Beyond simply sharing utility libraries and simple composition, HOCs are the best way to share behavior between React Components. If you find yourself writing a lot of code in different places that does the same thing, you may be able to refactor that code into a reusable HOC.

## Why do we need a key in the react?

Lists are an important aspect within your app. Every application is bound to make use of lists in some form or the other. You could have a list of tasks like a calendar app, list of pictures like Instagram, list of items to shop in a shopping cart and so on. The use-cases are numerous. Lists within an application can be performance heavy. Imagine an app with a huge list of videos or pictures and you keep getting thousands more, as you scroll. That could take a toll on the app’s performance.

Because performance is an important aspect, when you are using lists you need to make sure they are designed for optimal performance.

1. Lists are performant heavy and need to be used carefully.
2. Make sure every item in the list has a unique key.
3. It is prefered to not use indexes as a key unless you know for sure that the list is a static list (no additions/re-ordering/removal to the list).
4. Never use unstable keys like _Math.random()_ to generate a key.
5. React will run into performance degradation and unexpected behavior if unstable keys are used.

## What data flow does React follow?

It follows one-way data flow from higher order components to lower order components.

## Composition Over Inheritance, why?

In React, We always use Composition over Inheritance. We already discussed what is composition in the Functional programming section. This is a technique of combining simple reusable functions to generate a higher-order component. Here is an example of composition, we are using two small components `todoForm` and `todoList` in the dashboard component.

```jsx
import React from 'react';
import '../App.css';
import { ToDoForm } from './todoform';
import { ToDolist } from './todolist';

export class Dashboard extends React.Component {

  render() {
    return (
      <div className="dashboard"> 
          <ToDoForm />
          <ToDolist />
      </div>
    );
  }
}
```

## What are Error Boundaries?

In React, we usually have a component tree. If an error happens in any one of the components, it will break the whole component tree. There is no way of catching these errors. We can gracefully handle these errors with Error Boundaries.

Error Boundaries does two things

* display fallback UI if an error occurs
* lets you log errors

Here is an example of ErrorBoundary Class. Any class becomes ErrorBoundary if it implements any of these lifecycle methods `getDerivedStateFromError` or `componentDidCatch.` The former returns `{hasError: true}` to render the fallback UI and the latter is used to log the errors.

```jsx
import React from 'react'

export class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    // Update state so the next render will show the fallback UI.
    return { hasError: true };
  }

  componentDidCatch(error, info) {
    // You can also log the error to an error reporting service
    console.log('Error::::', error);
  }

  render() {
    if (this.state.hasError) {
      // You can render any custom fallback UI
      return <h1>OOPS!. WE ARE LOOKING INTO IT.</h1>;
    }

    return this.props.children; 
  }
}
```

Here is how we can use ErrorBoundary in one of the components. I am wrapping `ToDoForm` and `ToDoList` with the `ErrorBoundary` class. If any error occurs in these components we log the errors and display fallback UI.

```jsx
import React from 'react';
import '../App.css';
import { ToDoForm } from './todoform';
import { ToDolist } from './todolist';
import { ErrorBoundary } from '../errorboundary';

export class Dashboard extends React.Component {

  render() {
    return (
      <div className="dashboard"> 
        <ErrorBoundary>
          <ToDoForm />
          <ToDolist />
        </ErrorBoundary>
      </div>
    );
  }
}
```

## What are Fragments?

In React, we need to have a parent element while returning react elements from the component. Sometimes it is annoying to put an extra node into the DOM. With Fragments, we don’t have to put an extra node into the DOM. All we need to wrap the content with `React.Fragment` or with shorthand notation `<>.`

Here is an example. WithFragments, we don’t have to put an extra `div` if it’s not necessary.

```jsx
// Without Fragments   
return (
 <div>
    <CompoentA />
    <CompoentB />
    <CompoentC />
 </div>
)

// With Fragments   
return (
 <React.Fragment>
    <CompoentA />
    <CompoentB />
    <CompoentC />
 </React.Fragment>
)

// shorthand notation Fragments   
return (
 <>
    <CompoentA />
    <CompoentB />
    <CompoentC />
 </>
)
```

## What are prop-types and what are the benefits and drawbacks of them?

* Prop type is a way for you to know what types a component is expecting.
* They are great for when you want to know what a component needs to work!
* They often become legacy documentation and people forget to keep them updated or they put `.required` on the wrong things and often I see people use `.object` instead of `.shapeOf`
