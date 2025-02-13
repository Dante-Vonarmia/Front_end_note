# React Advanced

> React Hook

{% embed url="https://reactjs.org/docs/hooks-faq.html" %}

## What's the most important selling points of Hook of React?

* _Hooks_ are a new addition in React 16.8. They let you use state and other React features without writing a class.
* **Hooks allow you to reuse stateful logic without changing your component hierarchy.**
* Complex components become hard to understand, **Hooks let you split one component into smaller functions based on what pieces are related (such as setting up a subscription or fetching data)**, rather than forcing a split based on lifecycle methods.
* Classes confuse both people and machines, **hooks let you use more of React’s features without classes.**
* **Return to functional programming.**



> React Perfomance

## How do you handle bundling performance?

#### Good to hear&#x20;

* "There are loaders for it but mostly I try to reduce the bundling process"
* "I try to use a task runner and Webpack for bundling"

## When do you use server side rendering and why?

#### Good to hear

* "I used it in Node. Server side process/validate data. Client-end render/interact data"

## What is react performance profiling?

The concept of the [react profiler](https://reactjs.org/blog/2018/09/10/introducing-the-react-profiler.html) is to **collect timing information about components**, the time rendered and committed in order to identify when each component actually rendered and at what speed. Basically to explain to you how fast or how slow your application is.



> React Test

## When do you use component based testing and why?

#### Good to hear:

* "I use Enzyme but only for generic components since I use UI testing mostly"



> Advanced FAQs

## How to Apply Styles In React

{% embed url="https://blog.bitsrc.io/5-ways-to-style-react-components-in-2019-30f1ccc2b5b" %}

## How Does It Differ from Vue.js and Angular

{% embed url="https://vuejs.org/v2/guide/comparison.html" %}

## What is React Router and How It Works?

React Router is an API for React applications. Most current code is written with React Router 3, although version 4 has been released. React Router uses dynamic routing.

React Router, and dynamic, client-side routing, allows us to build a single-page web application with navigation without the page refreshing as the user navigates. React Router uses component structure to call components, which display the appropriate information.

By preventing a page refresh, and using Router or Link, which is explained in more depth below, the flash of a white screen or blank page is prevented. This is one increasingly common way of having a more seamless user experience. React router also allows the user to utilize browser functionality like the back button and the refresh page while maintaining the correct view of the application.

## What is the difference between React Native and React?

[ReactJS](https://facebook.github.io/react/) is a JavaScript library, supporting both front-end web and being run on a server, for building user interfaces and web applications. It follows the concept of reusable components.

[React Native](https://facebook.github.io/react-native/) is a mobile framework that makes use of JavaScript engine available on the host, allowing you to build mobile applications for different platforms (iOS, Android, and Windows Mobile) in JavaScript that allows you to use ReactJS to build reusable components and communicate with native components [further explanation](https://stackoverflow.com/questions/41124338/does-react-native-compile-javascript-into-java-for-android)

Both follow the JSX syntax extension to JavaScript. Which compiles to `React.createElement` calls under the hood. [JSX in-depth](https://reactjs.org/docs/jsx-in-depth.html)

Both are open-sourced by Facebook.

## How do you handle branding/themes?

#### Good to hear

* "I try to avoid them / I use a variant prop in the components"

## How do you handle translations?

#### Good to hear

* "We get them from an external tool"

## How do you make an API call from React?

#### How can I make an AJAX call? <a href="#how-can-i-make-an-ajax-call" id="how-can-i-make-an-ajax-call"></a>

You can use any AJAX library you like with React. Some popular ones are [Axios](https://github.com/axios/axios), [jQuery AJAX](https://api.jquery.com/jQuery.ajax/), and the browser built-in [window.fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API).

#### Where in the component lifecycle should I make an AJAX call? <a href="#where-in-the-component-lifecycle-should-i-make-an-ajax-call" id="where-in-the-component-lifecycle-should-i-make-an-ajax-call"></a>

You should populate data with AJAX calls in the [`componentDidMount`](https://reactjs.org/docs/react-component.html#mounting) lifecycle method. This is so you can use `setState` to update your component when the data is retrieved.
