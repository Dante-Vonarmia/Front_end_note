# Asynchronous

## What is asynchronous programming, and why is it important in JavaScript?

Synchronous programming means that, barring conditionals and function calls, code is executed sequentially from top-to-bottom, blocking on long-running tasks such as network requests and disk I/O.

Asynchronous programming means that the engine runs in an event loop. When a blocking operation is needed, the request is started, and the code keeps running without blocking for the result. When the response is ready, an interrupt is fired, which causes an event handler to be run, where the control flow continues. In this way, a single program thread can handle many concurrent operations.

User interfaces are asynchronous by nature, and spend most of their time waiting for user input to interrupt the event loop and trigger event handlers.

Node is asynchronous by default, meaning that the server works in much the same way, waiting in a loop for a network request, and accepting more incoming requests while the first one is being handled.

This is important in JavaScript, because it is a very natural fit for user interface code, and very beneficial to performance on the server.

**Good to hear:**

* An understanding of what blocking means, and the performance implications.
* An understanding of event handling, and why its important for UI code.

## What's the difference between a promise-based object and a generator-based object?

### Promise-based object&#x20;

The **`Promise`** object represents the eventual completion (or failure) of an asynchronous operation, and its resulting value.

A `Promise` is in one of these states:

* _pending_: initial state, neither fulfilled nor rejected.
* _fulfilled_: meaning that the operation completed successfully.
* _rejected_: meaning that the operation failed.

### Generator-based object

The **`Generator`** object is returned by a [generator function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function*) and it conforms to both the [iterable protocol](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#The_iterable_protocol) and the [iterator protocol](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#The_iterator_protocol).

## Is async/await the best way to implement the asynchronous programming?

Async/await basically act as syntactic sugar on top of promises, making asynchronous code easier to write and to read afterwards. They make async code look more like old-school synchronous code, so they're well worth learning.

_Generator functions/yield_ and _Async functions/await_ can both be used to write asynchronous code that “waits”, which means code that looks as if it was synchronous, even though it really is asynchronous.

_A generator function_ is executed **yield by yield** i.e one yield-expression at a time by its iterator (the `next` method) whereas &#x61;_&#x73;ync-await_, they are executed sequential **await by await**.

_Async/await_ makes it easier to implement a particular use case of _Generators_.

The return value of the &#x67;_&#x65;nerator_ is always **`{value: X, done: Boolean}`** whereas for &#x61;_&#x73;ync functions,_ it will always be a **promise** that will either resolve to the value X or throw an error.

An `async` function can be decomposed into a generator and promise implementation which is good to know stuff.
