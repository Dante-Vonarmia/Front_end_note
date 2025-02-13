---
description: Background Knowledge
---

# HTTP FAQs

### 1. What is HTTP?

* HTTP stands for Hypertext Transfer Protocol.&#x20;
* It is a set of rules for transferring of data on WWW (World Wide Web).

### 2. What are the basic Features of HTTP?

HTTP (Hypertext Transfer Protocol) is the protocol used for communication between a client (such as a web browser) and a server on the World Wide Web. Here are the basic features of HTTP:

1. Stateless: HTTP is a stateless protocol, which means that each request from a client to a server is treated as an independent request without any knowledge of previous requests. The server does not retain information about the client's previous requests or session state. However, mechanisms like cookies and sessions can be used to maintain stateful interactions.
2. Request/Response Model: HTTP follows a request/response model, where the client sends a request to the server, and the server responds with a corresponding response. The request typically includes a method (such as GET, POST, PUT, DELETE) to specify the desired action, along with headers and optional request body.
3. Uniform Resource Identifiers (URIs): HTTP uses URIs to identify and locate resources on the web. URIs, commonly referred to as URLs (Uniform Resource Locators), specify the address and path to a specific resource.
4. Methods: HTTP defines various methods that indicate the desired action to be performed on a resource. The most common methods are:
   * GET: Retrieve a resource from the server.
   * POST: Submit data to be processed by the server (e.g., form submissions).
   * PUT: Store or update a resource at a specified URI.
   * DELETE: Remove a specified resource from the server.
   * HEAD: Retrieve only the headers of a resource without the actual content.
5. Headers: HTTP headers provide additional information about the request or response. They can include details such as the content type, cache directives, authentication credentials, and more. Headers are used to pass information between the client and server.
6. Status Codes: HTTP uses status codes to indicate the outcome of a request. The status codes are three-digit numbers that classify responses into different categories, such as informational (1xx), success (2xx), redirection (3xx), client errors (4xx), and server errors (5xx).
7. Caching: HTTP supports caching, allowing clients and intermediate servers (proxies) to store and reuse responses for future requests. This helps reduce network traffic and improve performance by avoiding redundant transfers of unchanged resources.
8. Secure Communication: HTTP can be used over a secure connection using HTTPS (HTTP Secure). HTTPS employs encryption (TLS/SSL) to ensure confidentiality and integrity of data transmitted between the client and server. It adds a layer of security to protect sensitive information.\


### 3. What are request methods in HTTP?

Following are the request methods:

```
GET
```

It is used to send data in url.

```
POST
```

It is used to send data to the server.

```
PUT
```

It is used to send entire updated data to the server.

```
DELETE  
```

Delete method sends a request to the server to perform delete operation.

```
*HEAD*
```

It only transfers status line and header section as a request.

```
*CONNECT* 
```

It is used to establish connection to the server.

```
*OPTIONS* 
```

Option method describes communication options for target resource.

```
*TRACE* 
```

It performs message loop-back test along the path to the target resource.

### 4. What are the differences between GET and POST method?

Following are the differences between GET and POST method:

| Get                                                  | Post                                    |
| ---------------------------------------------------- | --------------------------------------- |
| It is cached.                                        | It cannot be cached.                    |
| It receives data using url in the browser.           | It does not send data into the url.     |
| It can receive limited amount of data to the server. | We can send data in bulk to the server. |

### 5. What is status code in HTTP?

It is a Standard response code given by web server on Internet.\
It helps to identify the cause of problem when web page or other resource does not load properly.

There are two major group of HTTP [status code](https://www.restapitutorial.com/httpstatuscodes.html) error exist:

* 4xx Client Error
* 5xx Server Error

### _6. What are the header fields in HTTP?_

HTTP headers fields allow the client and server to pass information with the request and response message.

Following are the header fields in HTTP:

#### General header

It applies for both request and response message.

#### Request header

It contains information for the request message.

#### Response header

It is used to contain response header information sent by the web server.

#### Entity header

It is used to contain more information about the body of the entity.

### _7. What is URI?_

URI (Uniform Resource Identifier) is used to define the identity of something on the web. It can represent a piece of a url.

### _8. What are_ [_Idempotent_](https://sofish.github.io/restcookbook/http%20methods/idempotency/) _methods?_

In idempotent methods, for the multiple requests, we get exact same result.\
It would no matter if the request is called one or ten times, the result should be same.

### _9. What is secure HTTP?_

* The secure HTTP is secure version of HTTP.&#x20;
* In this protocol, data transfer over the World Wide Web is secure and encrypted.&#x20;
* It is used to execute highly confidential online transaction like financial transactions.

### _10. What are the benefits of HTTPS certificate?_

The major benefits of HTTPS certificate are:

* Customer information like credit card number and ATM pin is encrypted and cannot be easily track. &#x20;
* Customers trust and prefer to purchase from the sites that use HTTPS protocol. &#x20;
* This protocol shows authenticate register domain as secure connection. &#x20;

### _11. What is cURL in HTTP?_

cURL is command line tool. It is available on all major operating systems.

