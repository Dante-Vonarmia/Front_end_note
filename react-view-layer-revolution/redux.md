# Redux

## When do you use Redux?

### **Same piece of application state needs to be mapped to multiple container components**.&#x20;

A good example of this is session state. When the app first loads, often information about the user needs to be shared with various components in the titlebar and each page. It’s likely these components don’t have any direct relationship so Redux provides a convenient way to share state.

### **Global components that can be accessed from anywhere.**&#x20;

It’s common to have components that live for the life of the application (for a single-page app this is every time the entry point is reloaded) that do things like show notifications, snackbars, tooltips, modals, interactive tutorials, etc. With Redux, you can create actions that dispatch commands to these components so, for example, if the code makes an asynchronous request to the backend it can dispatch a show snackbar action if the request fails. Without Redux, you would need some other event system or have to instantiate the snackbar component every time it gets used.

### **Too many props are being passed through multiple hierarchies of components.**&#x20;

If a higher-level component is provided with a dozen props and uses only two of them, and the rest are passed down to a lower-level component, then consider refactoring with Redux. This scenario happens a lot with wrapper components that just provide layout styles, but don’t require a lot of data or configuration. It’s more practical to side-chain Redux directly into a lower-level component in this case.

### **State management using setState is bloating the component.**&#x20;

This is pretty subjective, but components that are over several hundred lines of code start to become harder to reason and maintain. Separating out the state management into a reducer breaks up the code and makes it more readable.

### **Caching page state.**&#x20;

When the user does some stuff to a page, then goes to another page and comes back, the expectation usually is to have the page in the same state. Some of this can be addressed by saving the page state in the backend and recalling it on page load. But, often things like search input values and expanded/collapsed accordions are just overkill to store in the backend. Since reducers typically initialize and live throughout the session, they can cache the page state so things remain the same.

## Explain the compositions of Redux.

### Actions

**Actions** are payloads of information that send data from your application to your store. They are the _only_ source of information for the store. You send them to the store using [`store.dispatch()`](https://redux.js.org/api/store#dispatchaction).

Actions are plain JavaScript objects. Actions must have a `type` property that indicates the type of action being performed. Types should typically be defined as string constants. Once your app is large enough, you may want to move them into a separate module.

**Action creators** are exactly that—functions that create actions. It's easy to conflate the terms “action” and “action creator”, so do your best to use the proper term.

### Reducers

**Reducers** specify how the application's state changes in response to [actions](https://redux.js.org/basics/actions) sent to the store. Remember that actions only describe _what happened_, but don't describe how the application's state changes.

### Store

The **Store** is the object that brings them together. The store has the following responsibilities:

* Holds application state;
* Allows access to state via [`getState()`](https://redux.js.org/api/store#getState);
* Allows state to be updated via [`dispatch(action)`](https://redux.js.org/api/store#dispatchaction);
* Registers listeners via [`subscribe(listener)`](https://redux.js.org/api/store#subscribelistener);
* Handles unregistering of listeners via the function returned by [`subscribe(listener)`](https://redux.js.org/api/store#subscribelistener).

It's important to note that you'll only have a single store in a Redux application. When you want to split your data handling logic, you'll use [reducer composition](https://redux.js.org/basics/reducers#splitting-reducers) instead of many stores.\


## What is Redux Thunk used for?

Redux Thunk is a middleware that lets you call action creators that return a function instead of an action object. That function receives the store’s dispatch method, which is then used to dispatch regular synchronous actions inside the body of the function once the asynchronous operations have completed.

## Redux Thunk vs Redux Saga. What's the difference?

### Redux Thunk

* A thunk creator, which is an action creator that returns a thunk (a.k.a. asynchronous action creators)
* The thunk itself, which is the function that is returned from the thunk creator and accepts dispatch and setState as arguments.
* Redux-Thunk returns promises, which are more difficult to test. Testing thunks often requires complex mocking of the fetch api, axios requests, or other functions.
* The reason that we need to use a middleware such as Redux-Thunk is because the Redux store only supports synchronous data flow.&#x20;
* Middleware allows for asynchronous data flow, interprets anything that you dispatch and finally returns a plain object allowing the synchronous Redux data flow to resume. Redux middleware can thus solve for many critical asynchronous needs (e.g., axios requests).
* Redux-Thunk, however is great for small use cases and for beginners.The thunks’ logic is all contained inside of the function. Additionally, you do not need to learn a new function type, generators, and the keywords and methods associated with this function type.

### Redux Saga

* The benefit to Redux-Saga in comparison to Redux-Thunk is that you can avoid callback hell meaning that you can avoid passing in functions and calling them inside.&#x20;
* Additionally, you can more easily test your asynchronous data flow. The call and put methods return JavaScript objects. Thus, you can simply test each value yielded by your saga function with an equality comparison.  With Redux-Saga, you do not need to mock functions wrapped with effects. This makes tests clean, readable and easier to write.

In conclusion, there are tradeoffs for each middleware and depending on your project, you can decide which middleware is most fitting for your code.\


## How to Persist data when reloading the page?

{% embed url="https://css-tricks.com/one-way-to-break-users-out-of-the-habit-of-reloading-too-much/" %}
