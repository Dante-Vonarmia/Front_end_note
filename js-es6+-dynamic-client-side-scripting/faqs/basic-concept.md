# Core Mechanism

## Is JavaScript an Interpreted or a compiled language?

Yes, JavaScript (JS) is an interpreted language,\
still has its own form of a compiler, run in what’s known as the JavaScript engine(Chrome V8).

## Explain what is the operation mechanism of the JavaScript. (hint: event-loop, call-stack)

JavaScript has a concurrency model based on an event loop,\
which is responsible for executing the code, collecting and processing events, and executing queued sub-tasks.\
This model is quite different from models in other languages like C and Java.

JavaScript engine uses a **call stack** to manage [execution contexts:](../authors-notes/the-context.md#execution-context) the Global Execution Context and Function Execution Contexts.

At the most basic level, a call stack is a data structure that uses the Last In, First Out (LIFO) principle to temporarily store and manage function invocation (call).

**LIFO:** When we say that the call stack, operates by the data structure principle of Last In, First Out, it means that the last function that gets pushed into the stack is the first to be pop out, when the function returns.

{% hint style="info" %}
[Read more here](https://www.freecodecamp.org/news/understanding-the-javascript-call-stack-861e41ae61d4/)
{% endhint %}

## How context is different from the scope?

The scope is the accessibility of variables, functions, or objects in some particular part of your code during runtime.

Context is always the value of the `this` keyword which is a reference to the object that “owns” the currently executing code.

## How does the context behave in an execution context?

The value of `this` is determined at creation phase, not at the time of execution.  However, `this` determination rule remains the same.Is JavaScript an Interpreted or a compiled language?

Yes, Javascript (JS) is an interpreted language,\
still has its own form of a compiler, run in what’s known as the Javascript engine(Chrome V8).

JavaScript has a concurrency model based on an event loop,\
which is responsible for executing the code, collecting and processing events, and executing queued sub-tasks.\
This model is quite different from models in other languages like C and Java.

## Can you name two programming paradigms that are important for JavaScript developers?

JavaScript is a multi-paradigm language, supporting **imperative/procedural** programming along with **OOP** (Object-Oriented Programming) and **functional programming**. JavaScript supports OOP with **prototypal inheritance**.

#### **Good to hear:**

* Prototypal inheritance (also: prototypes, OLOO -- Object Linking to Other Objects).
* Functional programming (also: closures, first class functions, lambdas).

## When is classical inheritance an appropriate choice?

The answer is never, or almost never. Certainly never more than one level. Multi-level class hierarchies are an anti-pattern. I’ve been issuing this challenge for years, and the only answers I’ve ever heard fall into one of several [common misconceptions](https://medium.com/javascript-scene/common-misconceptions-about-inheritance-in-javascript-d5d9bab29b0a). More frequently, the challenge is met with silence.

#### **Good to hear:**

* Rarely, almost never, or never.
* A single level is sometimes OK, from a framework base-class such as `React.Component`.
* “Favor object composition over class inheritance.”

## When is prototypal inheritance an appropriate choice?

There is more than one type of prototypal inheritance:

* **Delegation** (i.e., the prototype chain).
* **Concatenative** (i.e. mixins, `Object.assign()`).
* **Functional** (Not to be confused with functional programming. A function used to create a closure for private state/encapsulation).

Each type of prototypal inheritance has its own set of use-cases, but all of them are equally useful in their ability to enable **composition,** which creates **has-a** or **uses-a** or **can-do** relationships as opposed to the **is-a** relationship created with class inheritance.

#### **Good to hear**:

* In situations where modules or functional programming don’t provide an obvious solution.
* When you need to compose objects from multiple sources.
* Any time you need inheritance.

## What is the difference between classical inheritance and prototypal inheritance?

**Class Inheritance:** instances inherit from classes (like a blueprint — a description of the class), and create sub-class relationships: hierarchical class taxonomies. Instances are typically instantiated via constructor functions with the `new` keyword. Class inheritance may or may not use the `class` keyword from ES6.

**Prototypal Inheritance:** instances inherit directly from other objects. Instances are typically instantiated via factory functions or `Object.create()`_._ Instances may be composed from many different objects, allowing for easy selective inheritance.

{% hint style="info" %}
In JavaScript, prototypal inheritance is simpler & more flexible than class inheritance.
{% endhint %}

#### **Good to hear:**

* Classes: create tight coupling or hierarchies/taxonomies.
* Prototypes: mentions of concatenative inheritance, prototype delegation, functional inheritance, object composition.

## What does “favor object composition over class inheritance” mean?

This is a quote from [“Design Patterns: Elements of Reusable Object-Oriented Software”](http://www.amazon.com/Design-Patterns-Elements-Reusable-Object-Oriented/dp/0201633612). It means that code reuse should be achieved by assembling smaller units of functionality into new objects instead of inheriting from classes and creating object taxonomies.

In other words, use **can-do, has-a,** or **uses-a** relationships instead of **is-a** relationships.

#### **Good to hear:**

* Avoid class hierarchies.
* Avoid brittle base class problem.
* Avoid tight coupling.
* Avoid rigid taxonomy (forced is-a relationships that are eventually wrong for new use cases).
* Avoid the gorilla banana problem (“what you wanted was a banana, what you got was a gorilla holding the banana, and the entire jungle”).
* Make code more flexible.

## List some OOP concept that is actually adopted in JavaScript.

* Objects
* Encapsulation
* Inheritance
* Instance
* ...

## What is `use strict` in JavaScript?

Strict Mode was a new feature in ECMAScript 5 that allows you to place a program, or a function, in a “strict” operating context. This strict context prevents certain actions from being taken and throws more exceptions. The statement “use strict”; instructs the browser to use the Strict mode, which is a reduced and safer feature set of JavaScript.

* Strict mode eliminates some JavaScript silent errors by changing them to throw errors.
* Strict mode fixes mistakes that make it difficult for JavaScript engines to perform optimizations: strict mode code can sometimes be made to run faster than identical code that’s not strict mode.
* Strict mode prohibits some syntax likely to be defined in future versions of ECMAScript.
* It prevents, or throws errors, when relatively “unsafe” actions are taken (such as gaining access to the global object).
* It disables features that are confusing or poorly thought out.
* Strict mode makes it easier to write “secure” JavaScript.
