# Function & Functional Programming

## What is functional programming?

Functional programming produces programs by composing mathematical functions and avoids shared state & mutable data. Lisp (specified in 1958) was among the first languages to support functional programming, and was heavily inspired by lambda calculus. Lisp and many Lisp family languages are still in common use today.

Functional programming is an essential concept in JavaScript (one of the two pillars of JavaScript). Several common functional utilities were added to JavaScript in ES5.

#### **Good to hear:**

* Pure functions / function purity.
* Avoid side-effects.
* Simple function composition.
* Examples of functional languages: Lisp, ML, Haskell, Erlang, Clojure, Elm, F Sharp, OCaml, etc…
* Mention of features that support FP: first-class functions, higher order functions, functions as arguments/values.

#### **Red flags:**

* No mention of pure functions / avoiding side-effects.
* Unable to provide examples of functional programming languages.
* Unable to identify the features of JavaScript that enable FP.

## What are the pros and cons of functional programming vs object-oriented programming?

**OOP Pros:** It’s easy to understand the basic concept of objects and easy to interpret the meaning of method calls. OOP tends to use an imperative style rather than a declarative style, which reads like a straight-forward set of instructions for the computer to follow.

**OOP Cons:** OOP Typically depends on shared state. Objects and behaviors are typically tacked together on the same entity, which may be accessed at random by any number of functions with non-deterministic order, which may lead to undesirable behavior such as race conditions.

**FP Pros:** Using the functional paradigm, programmers avoid any shared state or side-effects, which eliminates bugs caused by multiple functions competing for the same resources. With features such as the availability of point-free style (aka tacit programming), functions tend to be radically simplified and easily recomposed for more generally reusable code compared to OOP.

FP also tends to favor declarative and denotational styles, which do not spell out step-by-step instructions for operations, but instead concentrate on **what** to do, letting the underlying functions take care of the **how**. This leaves tremendous latitude for refactoring and performance optimization, even allowing you to replace entire algorithms with more efficient ones with very little code change. (e.g., memoize, or use lazy evaluation in place of eager evaluation.)

Computation that makes use of pure functions is also easy to scale across multiple processors, or across distributed computing clusters without fear of threading resource conflicts, race conditions, etc…

**FP Cons:** Over exploitation of FP features such as point-free style and large compositions can potentially reduce readability because the resulting code is often more abstractly specified, more terse, and less concrete.

More people are familiar with _OO_ and imperative programming than functional programming, so even common idioms in functional programming can be confusing to new team members.

FP has a much steeper learning curve than OOP because the broad popularity of OOP has allowed the language and learning materials of OOP to become more conversational, whereas the language of FP tends to be much more academic and formal. FP concepts are frequently written about using idioms and notations from lambda calculus, algebras, and category theory, all of which requires a prior knowledge foundation in those domains to be understood.

#### **Good to hear:**

* Mentions of trouble with shared state, different things competing for the same resources, etc…
* Awareness of FP’s capability to radically simplify many applications.
* Awareness of the differences in learning curves.
* Articulation of side-effects and how they impact program maintainability.
* Awareness that a highly functional codebase can have a steep learning curve.
* Awareness that a highly OOP codebase can be extremely resistant to change and very brittle compared to an equivalent FP codebase.
* Awareness that immutability gives rise to an extremely accessible and malleable program state history, allowing for the easy addition of features like infinite undo/redo, rewind/replay, time-travel debugging, and so on. Immutability can be achieved in either paradigm, but a proliferation of shared stateful objects complicates the implementation in OOP.

## What are IIFEs (Immediately Invoked Function Expressions)?



An **IIFE** (Immediately Invoked Function Expression) is a [JavaScript](https://developer.mozilla.org/en-US/docs/Glossary/JavaScript) [function](https://developer.mozilla.org/en-US/docs/Glossary/function) that runs as soon as it is defined.

```javascript
(function () {
    statements
})();
```

It is a design pattern which is also known as a [Self-Executing Anonymous Function](https://developer.mozilla.org/en-US/docs/Glossary/Self-Executing_Anonymous_Function) and contains two major parts:

1. The first is the anonymous function with lexical scope enclosed within the [`Grouping Operator`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Grouping) `()`. This prevents accessing variables within the IIFE idiom as well as polluting the global scope.
2. The second part creates the immediately invoked function expression `()` through which the JavaScript engine will directly interpret the function.

## What is the difference between anonymous and named functions?

Named functions are useful for a good debugging experience, while anonymous functions provides context scoping for easier development. Arrow functions should only be used when functions act as data.

## What is currying and how does it apply to a react application?&#x20;

It’s just a chaining styled format to passing down the multiples parameters which are usually callbacks functions. In React application. We usually use that as a HOC pattern. Or, while combining with redux, it’s common to connect the redux mapping props methods with the components.

## What is immutable data?

In [object-oriented](https://en.wikipedia.org/wiki/Object-oriented_computer_programming) and [functional](https://en.wikipedia.org/wiki/Functional_programming) programming, an **immutable object** (unchangeable[\[1\]](https://en.wikipedia.org/wiki/Immutable_object#cite_note-1) object) is an [object](https://en.wikipedia.org/wiki/Object_\(computer_science\)) whose state cannot be modified after it is created.

## What causes tight coupling? <a href="#id-7481" id="id-7481"></a>

### Tight coupling has many causes

* **Mutation** vs _immutability_
* **Side-Effects** vs _purity/isolated side-effects_
* **Responsibility overload** vs _Do One Thing (DOT)_
* **Procedural instructions** vs _describing structure_
* **Class Inheritance** vs _composition_

Imperative and object-oriented code is more susceptible to tight coupling than functional code. That doesn’t mean that programming in a functional style makes your code immune to tight coupling, but functional code uses pure functions as the elemental unit of composition, and pure functions are less vulnerable to tight coupling by nature.

### Pure functions

* Given the same input, always return the same output, and
* Produce no side-effects

### How do pure functions reduce coupling?

* **Immutability:** Pure functions don’t mutate existing values. They return new ones, instead.
* **No side effects:** The only observable effect of a pure function is its return value, so there’s no chance for it to interfere with the operation of other functions that may be observing external state such as the screen, the DOM, the console, standard out, the network, or the disk.
* **Do one thing:** Pure functions do one thing: Map some input to some corresponding output, avoiding the responsibility overload that tends to plague object and class-based code.
* **Structure, not instructions:** Pure functions can be safely memoized, meaning that, if the system had infinite memory, any pure function could be replaced with a lookup table that uses the function’s input as an index to retrieve a corresponding value from the table. In other words, pure functions describe structural relationships between data, not instructions for the computer to follow, so two different sets of conflicting instructions running at the same time can’t step on each other’s toes and cause problems.
