# React Components

## When would you use the class component rather than the functional component?

Everything is a component in React. We usually break up the entire logic of the application into small individual pieces. We call each individual piece as a component. In general, A component is a javascript function which takes the input, process it and returns React element which renders in the UI.

### Functional/Stateless/Presentational Components <a href="#b498" id="b498"></a>

A functional or stateless component is a pure function which takes props or no props and returns the react element. These are pure functions which don’t have any side effects. These components don’t have state or lifecycle methods. Here is an example.

```jsx
import React from 'react';
import Jumbotron from 'react-bootstrap/Jumbotron';

export const Header = () => {
    return(
        <Jumbotron style={{backgroundColor:'orange'}}>
            <h1>TODO App</h1>
        </Jumbotron>
    )
}
```

### Class/Stateful Components <a href="#e024" id="e024"></a>

Class or Stateful components have state and lifecycle methods and it can change the state of the component with the help of `this.setState()`. Class components are created by extending the `React.Component` and it is initialized in the constructor and might have child components as well. Here is an example.

```jsx
import React from 'react';
import '../App.css';
import { ToDoForm } from './todoform';
import { ToDolist } from './todolist';

export class Dashboard extends React.Component {

  constructor(props){
    super(props);

    this.state = {

    }
  }
  
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

## What is PureComponent? When to use PureComponent over Component?

`PureComponent` is exactly the same as Component except that it handles the `shouldComponentUpdate` method for us. When `props` or `state` changes, `PureComponent` will do a shallow comparison on both `props` and `state`. `Component` on the other hand won't compare current props and state to next out of the box. Thus, the component will re-render by default whenever `shouldComponentUpdate` is called.

When comparing previous `props` and `state` to next, a shallow comparison will check that primitives have the same value (eg, 1 equals 1 or that true equals true) and that the references are the same between more complex javascript values like objects and arrays.

It is good to prefer `PureComponent` over `Component` whenever we never mutate our objects.

## When do you use a pure component and when do you use a class?

Pure Components gives a considerable increase in performance because it reduces the number of render operation in the application which is a huge win for complex UI and therefore advised to use if possible. Also, there will be cases where you want to use the lifecycle methods of Component and in such cases, we cannot use stateless components.

#### Good to hear

* I favor using pure components because there is often no reason to use a class if I am not storing a state or using a life cycle event.

## What is the difference between a presentational component and a container component?

As a way to simplify the distinction, we can say **presentational components are concerned with the look**, **container components are concerned with making things work**.

For example, this is a presentational component. It gets data from its props, and just focuses on showing an element:

```jsx
const Users = props => (
  <ul>
    {props.users.map(user => (
      <li>{user}</li>
    ))}
  </ul>
)
```

On the other hand this is a container component. It manages and stores its own data, and uses the presentational component to display it.

```jsx
class UsersContainer extends React.Component {
  constructor() {
    this.state = {
      users: []
    }
  }

  componentDidMount() {
    axios.get('/users').then(users =>
      this.setState({ users: users }))
    )
  }

  render() {
    return <Users users={this.state.users} />
  }
}
```

## What is the difference between the stateful and stateless component?

Stateful component can contains the state object and event handling function, user actions as well.

Stateless components are simple functional component without having a local state but remember there is a hook in react to add state behavior in functional component as well.

## What components make for a good container candidate?

I try to only use containers on components that are a bit more complex because the container itself makes the component more complex and if I am only making a small component without any extra complexity the cost of the container is greater than simply not using a container.

## How do you handle component reuse? Know when make a new component?

React Components are a great way of writing reusable code. We can simply create a class and then just call its instances wherever we want. Still, there are a few cases that can leave developers searching for a better option. Some of these cases are:

* **Its not entirely your code —** Developers rarely work alone. They work in groups, sharing their on platforms like GitHub and Bit. So, the reusable component that you might be using in your app, might not be written by yourself. And that will stop you from tinkering with it, because you don’t want to generate numerous bugs which will take you even longer to fix.
* **Here, but not there** — You might also want to be selective about some of the behaviors of the reusable component. Meaning, you want it to render at some places with only certain behaviors enabled. So you can’t change the original component because then all the instances of the component will be changed. And if you decided to write a new component, then what’s the point of using reusable components anyways?

{% embed url="https://blog.bitsrc.io/reusable-components-in-react-a-practical-guide-ec15a81a4d71" %}

## What are controlled and uncontrolled components in React?

This relates to stateful DOM components (form elements) and the difference:

* A **Controlled Component** is one that takes its current value through props and notifies changes through callbacks like onChange. A parent component “controls” it by handling the callback and managing its own state and passing the new values as props to the controlled component. You could also call this a “dumb component”.
* A Uncontrolled Component is one that stores its own state internally, and you query the DOM using a ref to find its current value when you need it. This is a bit more like traditional HTML.

In most (or all) cases we should use controlled components.

## How do you handle multiple component variants in the same codebase?

{% embed url="https://12factor.net/codebase" %}

## How parent and child components communicate?

#### From Child to Parent with Callbacks

For a child to talk back to a parent (unacceptable, I know!), it must first receive a mechanism to communicate back from its parent. As we learned, parents pass data to children through `props`. A "special" prop of type `function` can be passed down to a child. At the time of a relevant event (eg, user interaction) the child can then call this function as a callback.

Let's say that a book can be edited from a `BookTitle` component:

```jsx
function BookTitle(props) {
  return (
    <label>
      Title: 
      <input onChange={props.onTitleChange} value={props.title} />
    </label>
  )
}
```

It receives a `onTitleChange` function in the `props`, sent from its parent. It binds this function to the `onChange` event on the `<input />` field. When the input changes, it will call the `onTitleChange` callback, passing the change `Event` object.

Because the parent, `BookEditForm`, has reference to this function, it can receive the arguments that are passed to the function:

```jsx
import React, { useState } from 'react'

function BookEditForm(props) {
  const [title, setTitle] = useState(props.book.title)
  function handleTitleChange(evt) {
    setTitle(evt.target.value)
  }
  return (
    <form>
      <BookTitle onTitleChange={handleTitleChange} title={title} />
    </form>
  )
}
```

In this case, the parent passed `handleTitleChange`, and when it's called, it sets the internal state based on the value of `evt.target.value` -- a value that has come as a callback argument from the child component.

There are some cases, however, when data sent through `props` might not be the best option for communicating between components. For these cases, React provides a mechanism called context.\


## Which life cycle event is the most common from your perspective?

{% embed url="https://blog.bitsrc.io/react-16-lifecycle-methods-how-and-when-to-use-them-f4ad31fb2282?source=bookmarks---------5------------------" %}

## What is render() in React? And explain its purpose? Explain it in your own terms.

Each React component must have a `render()` mandatorily. It returns a single React element which is the representation of the native DOM component. If more than one HTML element needs to be rendered, then they must be grouped together inside one enclosing tag such as `<form>`, `<group>`, `<div>` etc. This function must be kept pure i.e., it must return the same result each time it is invoked.

## **What are refs in React? When to use Refs?**

Refs are escape hatch that provides a direct way to access DOM nodes or React elements created in the render method.

Refs get in use when

* To manage focus, text selection, or media playback
* To trigger imperative animations
* To integrate with third-party DOM libraries

In order to use them you add a ref attribute to your component whose value is a callback function which will receive the underlying DOM element or the mounted instance of the component as its first argument.

```jsx
class UnControlledForm extends Component {
    handleSubmit = () => {
        console.log("Input Value: ", this.input.value)
    }
    
    render () {
        return (
            <form onSubmit={this.handleSubmit}>
                <input
                    type='text'
                    ref={(input) => this.input = input} 
                />
                <button type='submit'>Submit</button>
            </form>
        )
    }
}
```

Above notice that our input field has a ref attribute whose value is a function. That function receives the actual DOM element of input which we then put on the instance in order to have access to it inside of the handleSubmit function.

It’s often misconstrued that you need to use a class component in order to use refs, but refs can also be used with functional components by leveraging closures in JavaScript.

```jsx
function CustomForm ({handleSubmit}) {
    let inputElement
    return (
        <form onSubmit={() => handleSubmit(inputElement.value)}>
        <input
            type='text'
            ref={(input) => inputElement = input} />
        <button type='submit'>Submit</button>
        </form>
    )
}
```
