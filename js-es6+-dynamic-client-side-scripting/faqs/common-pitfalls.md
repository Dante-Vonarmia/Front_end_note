# Common pitfalls

## Why we need to avoid Global Variables and Functions?&#x20;

Global variables are easily overwritten by other scripts. For example when two separate parts of an application define global variables with the same name but with different purposes.

In JavaScript, it enables us to have multiple `var` statements anywhere in a function, and they all act as if the variables were declared at the top of the function.

It’s also common for web pages to include code not written by the developers of the page, for example.

* A third-party JavaScript library
* Code from a third-party user tracking and analytics script
* Different kinds of widgets, badges, and buttons
* Scripts from an advertising partner

## What are two-way data binding and one-way data flow, and how are they different?

Two way data binding means that UI fields are bound to model data dynamically such that when a UI field changes, the model data changes with it and vice-versa.

One way data flow means that the model is the single source of truth. Changes in the UI trigger messages that signal user intent to the model (or “store” in React). Only the model has the access to change the app’s state. The effect is that data always flows in a single direction, which makes it easier to understand.

One way data flows are deterministic, whereas two-way binding can cause side-effects which are harder to follow and understand.

**Good to hear:**

* React is the new canonical example of one-way data flow, so mentions of React are a good signal. Cycle.js is another popular implementation of uni-directional data flow.
* Angular is a popular framework which uses two-way binding.

## What are the pros and cons of monolithic vs microservice architectures?

A monolithic architecture means that your app is written as one cohesive unit of code whose components are designed to work together, sharing the same memory space and resources.

A microservice architecture means that your app is made up of lots of smaller, independent applications capable of running in their own memory space and scaling independently from each other across potentially many separate machines.

### **Monolithic Pros:**&#x20;

The major advantage of the monolithic architecture is that most apps typically have a large number of cross-cutting concerns, such as logging, rate limiting, and security features such audit trails and DOS protection.

When everything is running through the same app, it’s easy to hook up components to those cross-cutting concerns.

There can also be performance advantages, since shared-memory access is faster than inter-process communication (IPC).

### **Monolithic cons:**&#x20;

Monolithic app services tend to get tightly coupled and entangled as the application evolves, making it difficult to isolate services for purposes such as independent scaling or code maintainability.

Monolithic architectures are also much harder to understand, because there may be dependencies, side-effects, and magic which are not obvious when you’re looking at a particular service or controller.

### **Microservice pros:**&#x20;

Microservice architectures are typically better organized, since each microservice has a very specific job, and is not concerned with the jobs of other components. Decoupled services are also easier to recompose and reconfigure to serve the purposes of different apps (for example, serving both the web clients and public API).

They can also have performance advantages depending on how they’re organized because it’s possible to isolate hot services and scale them independent of the rest of the app.

### **Microservice cons:**&#x20;

As you’re building a new microservice architecture, you’re likely to discover lots of cross-cutting concerns that you did not anticipate at design time. A monolithic app could establish shared magic helpers or middleware to handle such cross-cutting concerns without much effort.

In a microservice architecture, you’ll either need to incur the overhead of separate modules for each cross-cutting concern, or encapsulate cross-cutting concerns in another service layer that all traffic gets routed through.

Eventually, even monolthic architectures tend to route traffic through an outer service layer for cross-cutting concerns, but with a monolithic architecture, it’s possible to delay the cost of that work until the project is much more mature.

Microservices are frequently deployed on their own virtual machines or containers, causing a proliferation of VM wrangling work. These tasks are frequently automated with container fleet management tools.

#### **Good to hear:**

* Positive attitudes toward microservices, despite the higher initial cost vs monolthic apps. Aware that microservices tend to perform and scale better in the long run.
* Practical about microservices vs monolithic apps. Structure the app so that services are independent from each other at the code level, but easy to bundle together as a monolithic app in the beginning. Microservice overhead costs can be delayed until it becomes more practical to pay the price.

## `preventDefault` vs. `stopPropagation` vs. `stopImmediatePropagation`

* **preventDefault:** Cancels the event if it is cancelable, without stopping further propagation of the event.
* **stopPropagation:** Prevents further propagation of the current event.
* **stopImmediatePropagation:** Prevents other listeners of the same event from being called.

## What kinds of codes do front-end actually divided from back-end is as an anti-pattern?

{% embed url="https://css-tricks.com/the-great-divide/" %}

## What are the responsibilities of front-end and back-end?

Well, the simplest answer for this question is:

* Front-end is for render data
* Back-end is for validate data

{% embed url="https://www.indeed.com/career-advice/career-development/front-end-vs-back-end" %}

## Shall we load the JavaScript Files first in an HTML file?

It is a best practice to put JavaScript \<script> tags just before the closing \</body> tag rather than in the \<head> section of your HTML.

The reason for this is that HTML loads from top to bottom. The head loads first, then the body, and then everything inside the body. If we put our JavaScript links in the head section, the entire JavaScript file will load before loading any of the HTML, which could cause a few problems.

1. If you have code in your JavaScript that alters HTML as soon as the JavaScript file loads, there won't actually be any HTML elements available for it to affect yet, so it will seem as though the JavaScript code isn't working, and you may get errors.
2. If you have a lot of JavaScript, it can visibly slow the loading for your page because it loads all of the JavaScript before it loads any of the HTML.
3. When placing JavaScript links at the bottom of your HTML body, it gives the HTML time to load before any of the JavaScript loads, which can prevent errors, and speed up website response time.

## Name some ways of how do you debug your codes?

### **Developer tools in modern web browsers**

* Outputting JavaScript debugging messages to the browser
* (legacy) Popping up messages with `alert()`
* Logging lines to console with `console.log()`
* Pausing code execution with the `debugger`
* Chrome developer tools
* React Developer Tools for Chrome
* Opera - Chromium Dev Tools (for unit testing)

### **ESLint**

[ESLint](https://eslint.org/) is a linter for JavaScript. Linters will analyze code as it is written and identify a variety of basic syntax problems.&#x20;

The use of ESLint will allow you to catch errors, particularly easy to resolve but annoying ones such as missing brackets or typos, before executing the code.&#x20;

### **Webpack**

[Webpack](https://webpack.js.org/) is a bundling tool used by developers for all manner of sites and applications. If you use Webpack to do your bundling, you have the advantage of the [stats data](https://webpack.js.org/api/stats/) available from the tool.

### **JSON Formatter and Validator**

The [JSON Formatter & Validator](https://jsonformatter.curiousconcept.com/) relieves that pain point, so we’ve added it to this list of what I feel are the best JavaScript debugging tools. Postman automatically formats the object and allows you to easily validate both its JSON syntax as well as the actual content. You simply paste your JSON in, and it outputs the correctly formatted version.

## In form elements. How do you trigger the status of a checkBox or a radioBox.

### JavaScript Checkbox

To get the state of a checkbox, whether checked or unchecked, you follow these steps:

* First, select the checkbox using the selecting DOM methods such as [`getElementById()`](https://www.javascripttutorial.net/javascript-dom/javascript-getelementbyid/) or [`querySelector()`](https://www.javascripttutorial.net/javascript-dom/javascript-queryselector/).
* Then, access the `checked` property of the checkbox element. If its `checked` property is `true`, then the checkbox is checked; otherwise, it is not.

Suppose that you have a checkbox like this:

```javascript
<input type="checkbox" id="accept"> Accept
```

To check if the `accept` checkbox is checked, you use the following code:

```javascript
const cb = document.getElementById('accept');
console.log(cb.checked);
```

Additionally, you can use use the `querySelector()` to check if the `:checked` selector does not return `null`, like this:

```javascript
document.querySelector('#accept:checked') !== null
```

If a checkbox does not have the `value` attribute, its default value is `'on'`:

```javascript
<input type="checkbox" id="accept">
```

If you get the `value` attribute of a checkbox, you always get the `'on'` string whether the checkbox is checked or not. For example:

```javascript
const cb = document.getElementById('accept');
console.log(cb.value); // on
```

### JavaScript Radio Button

Radio buttons allow you to select only one of a predefined set of mutually exclusive options. To create a radio button you use the `<input type="radio">` element. For example:

```javascript
<form>
    <input type="radio" name="choice" value="yes"> Yes
    <input type="radio" name="choice" value="no"> No
</form>
```

You use a name to form a group of radio buttons. In a group, you can only select one radio button.

To find the selected radio button, you use these steps:

* Select radio buttons by using DOM methods such as [`querySelectorAll()`](https://www.javascripttutorial.net/javascript-dom/javascript-queryselector/) method.
* Get the `checked` property of the radio button. If the `checked` property is `true`, the radio button is checked; otherwise, it is not.

To know which radio button is checked, you use the `value` attribute.

## Since we mentioned about "Performance". List all the strategy you know. (hint: engineering aspect)

* Rule 1: Make Fewer HTTP Requests
* Rule 2: Use a Content Delivery Network
* Rule 3: Add an Expires Header
* Rule 4: Gzip Components
* Rule 5: Put Stylesheets at the Top
* Rule 6: Put Scripts at the Bottom
* Rule 7: Avoid CSS Expressions
* Rule 8: Make JavaScript and CSS External
* Rule 9: Reduce DNS Lookups
* Rule 10: Minify JavaScript
* Rule 11: Avoid Redirects
* Rule 12: Remove Duplicate Scripts

## REST vs GraphQL. Try to explain what's the difference.

{% embed url="https://www.howtographql.com/basics/1-graphql-is-the-better-rest/" %}

## List all the design pattern you've learned and give a sample scenario for each of them.

```
Pattern Design (philosophy & experience)
Singleton               : (single dialogue frame)
Factory                 : (third-part animation plugins)
Strategy                : (reducer, dispatch)
Pub/Sub(Observer)       : (React)
Mediator                : (Redux)
Chain of Responsibility : (coupon system)
Flyweight               : (file upload, optimize performance)
```

## What does it mean: keep your code DRY? (hint: a term in code structure)

Don’t Repeat Yourself (DRY) is a software development principle, the main aim of which is to reduce repetition of code.

Write Everything Twice (WET) is a cheeky abbreviation to mean the opposite i.e. code that doesn’t adhere to DRY principle.

## Any ideas about modular asynchronous function programming strategy? (hint: AMD, CMD)

### CMD

Node.js is the main practitioner of the commonJS specification. It has four important environment variables to provide support for modular implementation: `module`, `exports`, `require`, and `global`. In actual use, use `module.exports` to define the output interface of the current module (`exports` are not recommended), and `require` to load the module.

CommonJS loads modules in a synchronous manner. On the server side, the module files are stored on the local disk and read very quickly, so there will be no problem in doing so. But on the browser side, due to network reasons, a more reasonable solution is to use asynchronous loading.

### AMD

The AMD specification loads the module asynchronously, and the loading of the module does not affect the operation of the statements that follow it. All statements that depend on this module are defined in a callback function. This callback function will not run until the loading is completed.

#### AMD Advantages:

* AMD modules are flexible.
* Plugin support (extremely useful and powerful).
* Can load more than just JavaScript files.
* Path aliases and other advanced config settings to simplify path resolution and dependency listing.
* Works in the browser without a build (most popular AMD loaders supports this feature).
* Is asynchronous by nature.
* Works in current browsers, no need to wait for Harmony.
* Dependencies are usually listed on the same location making it easy to identify what are the dependencies.
* Avoid globals by default since modules are wrapped by closures.
* Can run the same code on both environments by simply using an AMD loader that works on a CJS environment.
* Lazy-load scripts if needed.

{% embed url="https://addyosmani.com/resources/essentialjsdesignpatterns/book/#modularjavascript" %}

## Can you explain the difference between Debouncing and throttle in user experience?

### Throttling

Throttling enforces a maximum number of times a function can be called over time. As in “execute this function at most once every 100 milliseconds.”

### Debouncing

Debouncing enforces that a function will not be called again until a certain amount of time has passed since its last call. As in “execute this function only if an amount of time (ex. 100 milliseconds) have passed without it being called.”

## [3 Ways to Disable Copy Text in JavaScript & CSS](https://code-boxx.com/disable-copy-text-javascript-css/)

* Disable the right-click (context menu) to prevent copy-and-paste.
* Disable the clipboard copy.
* CSS disable select and hide the highlighting of text.

## [4 Ways To Abort JavaScript Execution](https://code-boxx.com/abort-javascript-execution/)

* Manually throw an error in a function.
* Run the script with workers that can be terminated.
* Simply return false or undefined in a function.
* Set the script to run on a timer, clear the time to stop running.
