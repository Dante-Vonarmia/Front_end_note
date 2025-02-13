# THE Context

## Execution Context

1. Global Execution Context
   * Create a ‘window’ object.
   * The window object is referenced to ‘this’ keyword.
2. Function Execution Context
   * Whenever the code execution found a function it creates a new function execution contexts.&#x20;

## Execution Stack / Call Stack

> Execution Context Phases

In short, execution context is the ‘environment’ or scope in which a function executes in.\
Every time a function is called, a new execution context is created.\
Every call to an execution context has 2 stages

* Creation Phase
  * A connection to the outer environment is created
  * Global environment: the outer environment is null
  * All functions and variables: form a scope chain all done in a memory of a web browser
  * Determined `this` keyword
* Activation(Execution) Phase
  * When the function is executed
  * Executed function will be popped off the stack and move onto the next one
  * `var` defined variables can be accessed before they are declared (though undefined)&#x20;
  * Variable hoisted / lifted: leaking `this`
