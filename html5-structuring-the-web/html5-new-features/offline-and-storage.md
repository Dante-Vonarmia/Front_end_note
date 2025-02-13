# Offline and storage

## Offline resources: The application cache

Firefox fully supports the HTML5 offline resource specification. Most others have offline resource support at some level.

## Online and offline events

Firefox 3 supports WHATWG online and offline events, which let applications and extensions detect whether or not there's an active Internet connection, as well as to detect when the connection goes up and down.

## WHATWG client-side session and persistent storage (aka DOM storage)

Client-side session and persistent storage allows web applications to store structured data on the client side.

## IndexedDB

IndexedDB is a web standard for the storage of significant amounts of structured data in the browser and for high performance searches on this data using indexes.

## Using files from web applications

Support for the new HTML5 File API has been added to Gecko, making it possible for web applications to access local files selected by the user. This includes support for selecting multiple files using the [`<input>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input) of [**type**](https://developer.mozilla.org/en-US/docs/HTML/Element/Input#attr-type) file HTML element's new [**multiple**](https://developer.mozilla.org/en-US/docs/HTML/Element/Input#attr-multiple) attribute. There also is [`FileReader`](https://developer.mozilla.org/en-US/docs/DOM/FileReader).

## Describe the difference between a `cookie`, `sessionStorage` and `localStorage`.

All the above-mentioned technologies are key-value storage mechanisms on the client side. They are only able to store values as strings.

|                                        | `cookie`                                                 | `localStorage` | `sessionStorage` |
| -------------------------------------- | -------------------------------------------------------- | -------------- | ---------------- |
| Initiator                              | Client or server. Server can use `Set-Cookie` header     | Client         | Client           |
| Expiry                                 | Manually set                                             | Forever        | On tab close     |
| Persistent across browser sessions     | Depends on whether expiration is set                     | Yes            | No               |
| Sent to server with every HTTP request | Cookies are automatically being sent via `Cookie` header | No             | No               |
| Capacity (per domain)                  | 4kb                                                      | 5MB            | 5MB              |
| Accessibility                          | Any window                                               | Any window     | Same tab         |

{% hint style="info" %}
_Note: If the user decides to clear browsing data via whatever mechanism provided by the browser, this will clear out any `cookie`, `localStorage`, or `sessionStorage` stored. It's important to keep this in mind when designing for local persistence, especially when comparing to alternatives such as server side storing in a database or similar (which of course will persist despite user actions)._
{% endhint %}

## What is the Application Cache in HTML5 and why it is used?

It's becoming increasingly important for web-based applications to be accessible offline. Yes, all browsers can cache pages and resources for long periods if told to do so, but the browser can kick individual items out of the cache at any point to make room for other things. HTML5 addresses some of the annoyances of being offline with the [ApplicationCache](http://www.whatwg.org/specs/web-apps/current-work/#applicationcache) interface.

Using the cache interface gives your application three advantages:

1. Offline browsing - users can navigate your full site when they're offline
2. Speed - resources come straight from disk, no trip to the network.
3. Resilience - if your site goes down for "maintenance" (as in, someone accidentally breaks everything), your users will get the offline experience

The Application Cache (or AppCache) allows a developer to specify which files the browser should cache and make available to offline users. Your app will load and work correctly, even if the user presses the refresh button while they're offline.

## Tell me two benefits of HTML5 Web Storag&#x65;_._

* It can store 5 to 10 MB data. That is far more than cookies.
* Web storage data never transferred with an HTTP request, so it increases the performance of the application.
* **Persist data in react on page refresh.**
