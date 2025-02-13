# Working Principles

## Explain CSS and how it works?

1. The browser loads the HTML (e.g. receives it from the network).
2. It converts the [HTML](https://developer.mozilla.org/en-US/docs/Glossary/HTML) into a [DOM](https://developer.mozilla.org/en-US/docs/Glossary/DOM) (_Document Object Model_). The DOM represents the document in the computer's memory. The DOM is explained in a bit more detail in the next section.
3. The browser then fetches most of the resources that are linked to by the HTML document, such as embedded images and videos ... and linked CSS! JavaScript is handled a bit later on in the process, and we won't talk about it here to keep things simpler.
4. The browser parses the fetched CSS, and sorts the different rules by their selector types into different "buckets", e.g. element, class, ID, and so on. Based on the selectors it finds, it works out which rules should be applied to which nodes in the DOM, and attaches style to them as required (this intermediate step is called a render tree).
5. The render tree is laid out in the structure it should appear in after the rules have been applied to it.
6. The visual display of the page is shown on the screen (this stage is called painting).

![The diagram offers a simple view of the process.](https://mdn.mozillademos.org/files/11781/rendering.svg)

## What is `rel` means in a `link` tag?

```markup
<link href="main.css" rel="stylesheet">
```

This simple example provides the path to the stylesheet inside an `href` attribute, and a `rel` attribute with a value of `stylesheet`. The `rel` stands for "relationship", and is probably one of the key features of the `<link>` element — the value denotes how the item being linked to is related to the containing document.&#x20;

## How does `@import` work?

The **`@import`** CSS at-rule is used to import style rules from other style sheets. These rules must precede all other types of rules, except `@charset` rules; as it is not a [nested statement](https://developer.mozilla.org/en-US/docs/Web/CSS/Syntax#nested_statements), `@import` cannot be used inside [conditional group at-rules](https://developer.mozilla.org/en-US/docs/Web/CSS/At-rule#Conditional_Group_Rules).

#### Syntax

```css
@import url;
@import url list-of-media-queries;
@import url supports( supports-query );
@import url supports( supports-query ) list-of-media-queries;
```

## How to apply CSS to the DOM?

> Different types of citing a CSS.

**Inline CSS:** Inline CSS contains the CSS property in the body section attached with element is known as inline CSS. This kind of style is specified within an HTML tag using the style attribute.

**Internal or Embedded CSS:** This can be used when a single HTML document must be styled uniquely. The CSS rule set should be within the HTML file in the head section i.e the CSS is embedded within the HTML file.

**External CSS:** External CSS contains separate CSS file which contains only style property with the help of tag attributes (For example class, id, heading, … etc). CSS property written in a separate file with .css extension and should be linked to the HTML document using **link** tag. This means that for each element, style can be set only once and that will be applied across web pages.

#### Or

Use JavaScript to control your CSS dynamically.
