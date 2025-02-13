---
description: https://developer.mozilla.org/en-US/docs/Learn/CSS/Howto/CSS_FAQ
---

# Project & Methodology

## Why doesn't my CSS, which is valid, render correctly?

Browsers use the `DOCTYPE` declaration to choose whether to show the document using a mode that is more compatible  with Web standards or with old browser bugs. Using a correct and modern `DOCTYPE` declaration at the start of your HTML will improve browser standards compliance.

Modern browsers have two main rendering modes:

* _Quirks Mode_: also called backwards-compatibility mode, allows legacy webpages to be rendered as their authors intended, following the non-standard rendering rules used by older browsers. Documents with an incomplete, incorrect, or missing `DOCTYPE` declaration or a known `DOCTYPE` declaration in common use before 2001 will be rendered in Quirks Mode.
* _Standards Mode_: the browser attempts to follow the W3C standards strictly. New HTML pages are expected to be designed for standards-compliant browsers, and as a result, pages with a modern `DOCTYPE` declaration will be rendered with Standards Mode.

Gecko-based browsers, have a third [_Almost Standards Mode_](https://developer.mozilla.org/en-US/docs/Gecko's_%22Almost_Standards%22_Mode) that has only a few minor quirks.

This is a list of the most commonly used `DOCTYPE` declarations that will trigger Standards or Almost Standards mode:

```markup
<!DOCTYPE html> /* This is the HTML5 doctype. Given that each modern browser uses an HTML5 
                   parser, this is the recommended doctype */

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.0 Transitional//EN"
"http://www.w3.org/TR/html4/loose.dtd">

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN"
"http://www.w3.org/TR/html4/strict.dtd">

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
```

When at all possible, you should just use the HTML5 doctype.

## Why don't my style rules work properly?

#### HTML elements hierarchy <a href="#html_elements_hierarchy" id="html_elements_hierarchy"></a>

#### Explicitly re-defined style rule <a href="#explicitly_re-defined_style_rule" id="explicitly_re-defined_style_rule"></a>

#### Use of a shorthand property <a href="#use_of_a_shorthand_property" id="use_of_a_shorthand_property"></a>

#### Use of the `*` selector <a href="#use_of_the_.2a_selector" id="use_of_the_.2a_selector"></a>

#### Specificity in CSS <a href="#specificity_in_css" id="specificity_in_css"></a>

## Explain BEM? OOCSS?

### BEM

BEM is a specific concrete application of OOCSS. BEM stands for Block Element Modifier, and it describes the pattern of each CSS object's class name. We use a modified form of BEM, described best by CSS Wizardry's post titled MindBEMding.

Essentially, each BEM class starts with a block, which is an object name. Let's start with `.byline`. Then, for children of that block, you add an element, separating it with two underscores: `.byline__name`. Finally, you can modify any class (block or element) by adding a modifier, separated with two hyphens: `.byline--expanded`.

### OOCSS

OOCSS is a programming paradigm. OOCSS stands for Object Oriented CSS, so it's best understood in the context of Object Oriented programming: classic (spaghetti) CSS vs. OOCSS is a bit like procedural (spaghetti) backend code vs. Object-Oriented backend code.

OOCSS focuses on flexible, modular, swappable components that do One Thing Well. OOCSS focuses on the [single responsibility principle](http://en.wikipedia.org/wiki/Single_responsibility_principle), [separation of concerns](http://en.wikipedia.org/wiki/Separation_of_concerns), and much more of the foundational concepts of Object Oriented Programming.

For a great introduction to OOCSS, [this post on the OOCSS Media Object](http://www.stubbornella.org/content/2010/06/25/the-media-object-saves-hundreds-of-lines-of-code/) (written by the/one of the people behind OOCSS) shows an example of what a CSS object looks like, and some of the benefits of using one.

## What's the difference between "resetting" and "normalizing" CSS? Which would you choose, and why?How to use filters in CSS

* **Resetting** - Resetting is meant to strip all default browser styling on elements. For e.g. `margin`s, `padding`s, `font-size`s of all elements are reset to be the same. You will have to redeclare styling for common typographic elements.
* **Normalizing** - Normalizing preserves useful default styles rather than "unstyling" everything. It also corrects bugs for common browser dependencies.

I would choose resetting when I have a very customized or unconventional site design such that I need to do a lot of my own styling and do not need any default styling to be preserved.

## What existing CSS frameworks have you used locally, or in production? How would you change/improve them?

* **Bootstrap** - Slow release cycle. Bootstrap 4 has been in alpha for almost 2 years. Add a spinner button component, as it is widely used.
* **Semantic UI** - Source code structure makes theme customization extremely hard to understand. Its unconventional theming system is a pain to customize. Hardcoded config path within the vendor library. Not well-designed for overriding variables unlike in Bootstrap.
* **Bulma** - A lot of non-semantic and superfluous classes and markup required. Not backward compatible. Upgrading versions breaks the app in subtle manners.

## What are the advantages/disadvantages of using CSS preprocessors?

**Advantages:**

* CSS is made more maintainable.
* Easy to write nested selectors.
* Variables for consistent theming. Can share theme files across different projects.
* Mixins to generate repeated CSS.
* Sass features like loops, lists, and maps can make configuration easier and less verbose.
* Splitting your code into multiple files. CSS files can be split up too but doing so will require an HTTP request to download each CSS file.

**Disadvantages:**

* Requires tools for preprocessing. Re-compilation time can be slow.
* Not writing currently and potentially usable CSS. For example, by using something like [postcss-loader](https://github.com/postcss/postcss-loader) with [webpack](https://webpack.js.org/), you can write potentially future-compatible CSS, allowing you to use things like CSS variables instead of Sass variables. Thus, you're learning new skills that could pay off if/when they become standardized.

## Describe Block Formatting Context (BFC) and how it works.

A Block Formatting Context (BFC) is part of the visual CSS rendering of a web page in which block boxes are laid out. Floats, absolutely positioned elements, `inline-blocks`, `table-cells`, `table-caption`s, and elements with `overflow` other than `visible` (except when that value has been propagated to the viewport) establish new block formatting contexts.

Knowing how to establish a block formatting context is important, because without doing so, the containing box will not [contain floated children](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Block_formatting_context#Make_float_content_and_alongside_content_the_same_height). This is similar to collapsing margins, but more insidious as you will find entire boxes collapsing in odd ways.

A BFC is an HTML box that satisfies at least one of the following conditions:

* The value of `float` is not `none`.
* The value of `position` is neither `static` nor `relative`.
* The value of `display` is `table-cell`, `table-caption`, `inline-block`, `flex`, or `inline-flex`.
* The value of `overflow` is not `visible`.

In a BFC, each box's left outer edge touches the left edge of the containing block (for right-to-left formatting, right edges touch).

Vertical margins between adjacent block-level boxes in a BFC collapse. Read more on [collapsing margins](https://www.sitepoint.com/web-foundations/collapsing-margins/).

## What are the various clearing techniques and which is appropriate for what context?

* Empty `div` method - `<div style="clear:both;"></div>`.
* Clearfix method - Refer to the `.clearfix` class above.
* `overflow: auto` or `overflow: hidden` method - Parent will establish a new block formatting context and expand to contains its floated children.

In large projects, I would write a utility `.clearfix` class and use them in places where I need it. `overflow: hidden` might clip children if the children is taller than the parent and is not very ideal.

## What are the different ways to visually hide content (and make it available only for screen readers)?

These techniques are related to accessibility (a11y).

* `width: 0; height: 0`. Make the element not take up any space on the screen at all, resulting in not showing it.
* `position: absolute; left: -99999px`. Position it outside of the screen.
* `text-indent: -9999px`. This only works on text within the `block` elements.
* Metadata. For example by using Schema.org, RDF, and JSON-LD.
* WAI-ARIA. A W3C technical specification that specifies how to increase the accessibility of web pages.

Even if WAI-ARIA is the ideal solution, I would go with the `absolute` positioning approach, as it has the least caveats, works for most elements and it's an easy technique.
