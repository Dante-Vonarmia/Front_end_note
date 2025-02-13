---
description: DOM events / BOM / JSON / Web APIs / RESTful APIs
---

# Events and APIs

## What is Cross-Origin Resource Sharing (CORS)? And how does it works?

CORS is a **security mechanism** that allows a web page from one domain or Origin to access a resource with a different domain (**cross-domain request).**

Without features like CORS, websites are **restricted** to accessing resources from the same origin through what is known as **same-origin policy.**

There are often cases where you need to make AJAX (i.e., Axios) calls to `https://api.mydomain.com` or `https://mydomain` incorporates your Node.js server or some 3rd party fonts or analytics providers like Google Analytics. **Cross-Origin Resource Sharing (CORS)** enables these cross-domain request&#x73;**.**

> Allow Cross domain request, bypassing same-origin policy

## What is **same-origin policy?** <a href="#id-9e0a" id="id-9e0a"></a>

The **same-origin policy** is a critical security mechanism that restricts how a document or script loaded from one origin can interact with a resource from another origin

It helps isolate potentially **malicious** document, reducing possible attack vectors such as **CSRF attack**

> same-origin policy is security model for web application

## What is the definition of ‘origin’? <a href="#id-8148" id="id-8148"></a>

At this point, Someone might wonder the definition of **origin** 🤔

**Origin** includes the combination of protocol, domain, and port. In other words,

The following URLs are different origins

```
https://www.google.com vs. https://www.api.google.comhttp://localhost:9000 vs. http://localhost:8080
```

While the following URLs are same origins

```
http://www.example.com/dir/page.html 
vs. 
http://www.example.com/dir/page2.html
```

![](<../../.gitbook/assets/image (1).png>)

## How CORS works <a href="#id-85b4" id="id-85b4"></a>

There are 2 types of CORS requests

1. simple requests
2. preflighted requests

### **1.Simple requests**

CORS request that does not require a preflight request

**Step 1**

A browser tab open to `https://www.mydomain.com` initiates AJAX request `GET` to `https://api.domains.com/widgets`

**Step 2**

Along with adding headers like `Host` , the browser automatically adds the `Origin` Request Header for cross-origin requests

![](<../../.gitbook/assets/Screen Shot 2020-07-19 at 6.40.11 PM.png>)

**Step 3**

The server checks the `Origin` request header. If the Origin value is allowed, it sets the `Access-Control-Allow-Origin` to the value in the request header `Origin`

![](<../../.gitbook/assets/Screen Shot 2020-07-19 at 6.42.42 PM.png>)

**Step 4**

When the browser receives the response, the browser checks the `Access-Control-Allow-Origin` header to see if it matches the origin of the tab

If not, the response is blocked

```
Access-Control-Allow-Origin: * allows all origins
--> a large security risk
```

### **2. Preflighted requests**

A preflighted request is a CORS request where the browser is required to send a **preflight** request before sending the request being **preflighted to ask the server permission if the original CORS request can proceed**

**Any CORS request has to be preflighted if**

* **AJAX call to POST JSON data to a REST API meaning the `Content-Type` header is `application/json` → RESTful API request**
* AJAX call to an API which uses a token to authenticate the API in a request header such `Authorization` → **authorized request using token**

**Step 1**

The browser sends the `OPTIONS` request first (aka the preflight request)

![](<../../.gitbook/assets/Screen Shot 2020-07-19 at 6.43.33 PM.png>)

**Step 2**

The server respond back specifying the allowed HTTP methods and headers. If the original CORS request intended to send a header or HTTP method not in the list, **failed**

![](<../../.gitbook/assets/Screen Shot 2020-07-19 at 6.44.11 PM.png>)

**Step 3**

Since the **headers and method** pass the check `200 OK` , the browser sends the original CORS request ( `Origin` header in the request)

![](<../../.gitbook/assets/Screen Shot 2020-07-19 at 6.45.01 PM.png>)

**Step 4**

The response has the correct origin in `Access-Control-Allow-Origin` header so checks pass and control is handed back to the browser tab

![](<../../.gitbook/assets/Screen Shot 2020-07-19 at 6.45.30 PM.png>)

## Give some samples of Browser Object Model (BOM).

| Reference                     | Object                                                                             |
| ----------------------------- | ---------------------------------------------------------------------------------- |
| window                        | The main browser window                                                            |
| window.navigator              | Information about the browser itself                                               |
| window.screen                 | The user's screen                                                                  |
| window.history                | URLs visited by a user                                                             |
| window.location               | The current URL                                                                    |
| window.document (document)    | The document appearing in the main browser window                                  |
| document.getElementById("id") | An HTML element appearing in a document and identified by its assigned _id_ value. |

## Explain RESTful API. What's the main features and why they're important?

REST is stands for REpresentational State Transfer; \
it's all about communication of state, and structured in terms of the resources which achieve this.

Good REST APIs are good software; \
they are simultaneously good consumer products, with the understanding that their consumers are application programmers.

Good APIs know their version\
providing the version as a paramete&#x72;**,** specifying it in the header.

Good REST APIs:

* Result paginate, filtering, sorting & searching
* are well-documented and reliable
* use HTTP verbs as Fielding originally defined
* support X-HTTP-METHOD-Override to accommodate picky proxies
* express URLs with nouns rather than verbs
* track version
* make expressive use of HTTP Status Codes
* handle errors carefully and explicitly
* log activity
* choose wisely between XML (increasingly rare), JSON, and HATEOAS (rapidly growing)
* Limiting which fields are returned by the API
* explicitly design in other commercially-significant API-specific features

## Explain Event target, Event Bubbling and Event Capturing ?

The standard [DOM Events](http://www.w3.org/TR/DOM-Level-3-Events/) describes 3 phases of event propagation:

1. Capturing phase – the event goes down to the element.
2. Target phase – the event reached the target element.
3. Bubbling phase – the event bubbles up from the element.

### Event Bubbling

The process is called “bubbling”, because events “bubble” from the inner element up through parents like a bubble in the water.

When an event happens on an element, it first runs the handlers on it, then on its parent, then all the way up on other ancestors.

### Event Capturing

There’s another phase of event processing called “capturing”. It is rarely used in real code, but sometimes can be useful.

**Before we only talked about bubbling, because the capturing phase is rarely used. Normally it is invisible to us.**

To catch an event on the capturing phase, we need to set the handler `capture` option to `true`:

```javascript
elem.addEventListener(..., {capture: true})
// or, just "true" is an alias to {capture: true}
elem.addEventListener(..., true)
```

There are two possible values of the `capture` option:

* If it’s `false` (default), then the handler is set on the bubbling phase.
* If it’s `true`, then the handler is set on the capturing phase.

#### Example of Bubbling and Capturing

```javascript
for(let elem of document.querySelectorAll('*')) {
  elem.addEventListener("click", e => alert(`Capturing: ${elem.tagName}`), true);
  elem.addEventListener("click", e => alert(`Bubbling: ${elem.tagName}`));
}
```

### Event target

A handler on a parent element can always get the details about where it actually happened.

**The most deeply nested element that caused the event is called a&#x20;**_**target**_**&#x20;element, accessible as `event.target`.**

Note the differences from `this` (=`event.currentTarget`):

* `event.target` – is the “target” element that initiated the event, it doesn’t change through the bubbling process.
* `this` – is the “current” element, the one that has a currently running handler on it.

For instance, if we have a single handler `form.onclick`, then it can “catch” all clicks inside the form. No matter where the click happened, it bubbles up to `<form>` and runs the handler.

In `form.onclick` handler:

* `this` (=`event.currentTarget`) is the `<form>` element, because the handler runs on it.
* `event.target` is the actual element inside the form that was clicked.

