# CSS Selectors

## Pseudo-class VS Pseudo-elements?

&#x20;This group of selectors includes pseudo-classes, which style certain states of an element. The `:hover` pseudo-class for example selects an element only when it is being hovered over by the mouse pointer.

As for pseudo-elements, which select a certain part of an element rather than the element itself.

## What is the difference between `id` and `class`?

#### ID’s are unique

* Each element can have only one ID
* Each page can have only one element with that ID

ID’s have special browser functionality, this is an important reason right here why having ID’s be absolutely unique is important. So your browser knows where to scroll!

#### Classes are _not_ unique

* It is allow to use the same class on multiple elements.
* It is allow to multiple classes on the same element.

## Explain how a browser determines what elements match a CSS selector.

This part is related to the above about [writing efficient CSS](https://github.com/yangshun/front-end-interview-handbook/blob/master/contents/en/css-questions.md#what-are-some-of-the-gotchas-for-writing-efficient-css). Browsers match selectors from rightmost (key selector) to left. Browsers filter out elements in the DOM according to the key selector and traverse up its parent elements to determine matches. The shorter the length of the selector chain, the faster the browser can determine if that element matches the selector.

For example with this selector `p span`, browsers firstly find all the `<span>` elements and traverse up its parent all the way up to the root to find the `<p>` element. For a particular `<span>`, as soon as it finds a `<p>`, it knows that the `<span>` matches and can stop its matching.

## Describe pseudo-elements and discuss what they are used for.

A CSS pseudo-element is a keyword added to a selector that lets you style a specific part of the selected element(s). They can be used for decoration (`:first-line`, `:first-letter`) or adding elements to the markup (combined with `content: ...`) without having to modify the markup (`:before`, `:after`).

* `:first-line` and `:first-letter` can be used to decorate text.
* Used in the `.clearfix` hack as shown above to add a zero-space element with `clear: both`.
* Triangular arrows in tooltips use `:before` and `:after`. Encourages separation of concerns because the triangle is considered part of styling and not really the DOM.
