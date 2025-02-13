# Basic text-level semantics

## What is semantic in HTML?

### Definition

In HTML, for example, the [`<h1>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/h1) element is a semantic element, which gives the text it wraps around the role (or meaning) of "a top level heading on your page."

```markup
<h1>This is a top level heading</h1>
```

By default, most browser's [user agent stylesheet](https://developer.mozilla.org/en-US/docs/Web/CSS/Cascade#User-agent_stylesheets) will style an [`<h1>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/h1) with a large font size to make it _look_ like a heading (although you could style it to look like anything you wanted).

On the other hand, you could make any element _look_ like a top level heading. Consider the following:

```markup
<span style="font-size: 32px; margin: 21px 0;">Is this a top level heading?</span>
```

This will render it to look like a top level heading, but it has no semantic value, so it will not get any extra benefits as described above. It is therefore a good idea to use the right HTML element for the right job.

HTML should be coded to represent the _data_ that will be populated and not based on its default presentation styling. Presentation (how it should look), is the sole responsibility of [CSS](https://developer.mozilla.org/en-US/docs/Web/CSS).

### Some of the benefits from writing semantic markup are as follows:

* Search engines will consider its contents as important keywords to influence the page's search rankings (see [SEO](https://developer.mozilla.org/en-US/docs/Glossary/SEO))
* Screen readers can use it as a signpost to help visually impaired users navigate a page
* Finding blocks of meaningful code is significantly easier than searching though endless `div`s with or without semantic or name-spaced classes.
* Suggests to the developer the type of data that will be populated.
* Semantic naming mirrors proper custom element/component naming.

{% hint style="info" %}
When approaching which markup to use, ask yourself:
{% endhint %}

* What element(s) best describe/represent the data that I'm going to populate?
* Is it a list of data?; ordered, unordered?
* Is it an article with sections and an aside of related information?
* Does it list out definitions?
* Is it a figure or image that needs a caption?
* Should it have a header and a footer in addition to the global site-wide header and footer?

## The Div VS the Paragraph element, what's the difference?

{% hint style="info" %}
\<div> is actually a [**non-semantic wrappers**](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/Document_and_website_structure#Non-semantic_wrappers)
{% endhint %}

A `<div>` element is designed to describe when come across a situation where you can't find an ideal semantic element to group some items together or wrap some content. Sometimes you might want to just group a set of elements together to affect them all as a single entity with some CSS or JavaScript.

A `<p>` element is designed to describe a **paragraph** of content. We cannot layout the entire site in a `<p>` element, that would be wrong semantically because the elements you use should give some meaning to the content (semantics) and not simply used as a tool to lay out the content.

## How to stress or emphasize content?&#x20;

### Emphasis

In HTML we use the [`<em>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/em) (emphasis) element to mark up such instances.

### Strong importance

In HTML we use the [`<strong>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/strong) (strong importance) element to mark up such instances.&#x20;

### Italic, bold, underline...

HTML5 redefined `<b>`, `<i>` and `<u>` with new, semantic roles.

* [`<i>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/i) is used to convey a meaning traditionally conveyed by italic: Foreign words, taxonomic designation, technical terms, a thought...
* [`<b>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/b) is used to convey a meaning traditionally conveyed by bold: Key words, product names, lead sentence...
* [`<u>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/u) is used to convey a meaning traditionally conveyed by underline: Proper name, misspelling...

{% hint style="info" %}
The concept of **italics** isn't very helpful to people using screen readers, or to people using a writing system other than the Latin alphabet.
{% endhint %}

## How to display computer code with HTML?

* [`<code>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/code): For marking up generic pieces of computer code.
* [`<pre>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/pre): For retaining whitespace (generally code blocks) — if you use indentation or excess whitespace inside your text, browsers will ignore it and you will not see it on your rendered page. If you wrap the text in `<pre></pre>` tags however, your whitespace will be rendered identically to how you see it in your text editor.
* [`<var>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/var): For specifically marking up variable names.
* [`<kbd>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/kbd): For marking up keyboard (and other types of) input entered into the computer.
* [`<samp>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/samp): For marking up the output of a computer program.

## How to mark abbreviations and make them understandable

Another fairly common element you'll meet when looking around the Web is [`<abbr>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/abbr) — this is used to wrap around an abbreviation or acronym, and provide a full expansion of the term (included inside a [`title`](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes#attr-title) attribute.) Let's look at a couple of examples:

```markup
<p>We use <abbr title="Hypertext Markup Language">HTML</abbr> to structure our web documents.</p>

<p>I think <abbr title="Reverend">Rev.</abbr> Green did it in the kitchen with the chainsaw.</p>
```

## How to build a description list?

Description list is a special definition of list in HTML.&#x20;

Description lists are just what they claim to be: a list of terms and their matching descriptions (e.g., definition lists, dictionary entries, FAQs, and key-value pairs).

The terms described go inside [`<dt>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/dt) elements. \
The matching description follows immediately, contained within one or more [`<dd>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/dd) elements. \
Enclose the whole description list with a [`<dl>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/dl) element.

{% hint style="info" %}
In real environment developer prefer to construct comments section or thumbnails with a description list. More details about [terms definition](https://developer.mozilla.org/en-US/docs/Learn/HTML/Howto/Define_terms_with_HTML).
{% endhint %}

## Describe the difference between `<script>`, `<script async>` and `<script defer>`.

* `<script>` - HTML parsing is blocked, the script is fetched and executed immediately, HTML parsing resumes after the script is executed.
* `<script async>` - The script will be fetched in parallel to HTML parsing and executed as soon as it is available (potentially before HTML parsing completes). Use `async` when the script is independent of any other scripts on the page, for example, analytics.
* `<script defer>` - The script will be fetched in parallel to HTML parsing and executed when the page has finished parsing. If there are multiple of them, each deferred script is executed in the order they were encoun­tered in the document. If a script relies on a fully-parsed DOM, the `defer` attribute will be useful in ensuring that the HTML is fully parsed before executing. There's not much difference in putting a normal `<script>` at the end of `<body>`. A deferred script must not contain `document.write`.

{% hint style="info" %}
Note: The `async` and `defer` attrib­utes are ignored for scripts that have no `src` attribute.
{% endhint %}
