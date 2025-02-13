# Styling Syntax

## Name new feature modules which are used in CSS3.

#### There are several modules in CSS as stated below:

* Selectors
* Box Model
* Backgrounds and Borders
* Text Effects
* 2D/3D Transformations
* Animations
* Multiple Column Layout
* User Interface.

## How would you implement a web design comp that uses non-standard fonts?

Use `@font-face` and define `font-family` for different `font-weight`s.

## How to get different font?

*   The best approach is to always have at least two fonts in your [font stack](https://www.lifewire.com/font-stack-definition-3467414) (the list of fonts), so that if the browser doesn’t have the first font, it can use the second font instead.

    Separate multiple font choices with a comma, like this:

    ```css
    font-family: Arial, Geneva, Helvetica, sans-serif; 
    ```
*   The example outlined above uses inline styling, but the best [kind of styling](https://www.lifewire.com/types-of-css-styles-3466921) uses an [external style sheet](https://www.lifewire.com/what-is-an-external-style-sheet-4685757) to modify more than just the one element. Use a class to set the style on blocks of text.&#x20;

    ```markup
    <div class="arial"><p>This text is in Arial</p></div>
    ```

    In this example, the CSS file to style the above HTML would appear as follows:

    ```css
    .arial { font-family: Arial; } 
    ```
* Always end CSS styles with a semicolon (;). It's not required when there's only one style, but it's a good habit to start.

## What are the main properties for styling images?

* The `src` attribute is **required**, and contains the path to the image you want to embed.
* The `alt` attribute holds a text description of the image, which isn't mandatory but is **incredibly useful** for accessibility — screen readers read this description out to their users so they know what the image means. Alt text is also displayed on the page if the image can't be loaded for some reason: for example, network errors, content blocking.

## How do we styling tables in web page? Any common properties?

* Make your table markup as simple as possible, and keep things flexible, e.g. by using percentages, so the design is more responsive.
* Use [`table-layout`](https://developer.mozilla.org/en-US/docs/Web/CSS/table-layout)`: fixed` to create a more predictable table layout that allows you to easily set column widths by setting [`width`](https://developer.mozilla.org/en-US/docs/Web/CSS/width) on their headings ([`<th>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/th)).
* Use [`border-collapse`](https://developer.mozilla.org/en-US/docs/Web/CSS/border-collapse)`: collapse` to make table elements borders collapse into each other, producing a neater and easier to control look.
* Use [`<thead>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/thead), [`<tbody>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/tbody), and [`<tfoot>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/tfoot) to break up your table into logical chunks and provide extra places to apply CSS to, so it is easier to layer styles on top of one another if required.
* Use zebra striping to make alternative rows easier to read.
* Use [`text-align`](https://developer.mozilla.org/en-US/docs/Web/CSS/text-align) to line up your [`<th>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/th) and [`<td>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/td) text, to make things neater and easier to follow.

## All value units: `px` VS `pt` VS `em` and `rem` etc.

**Absolute length units**

The following are all **absolute** length units — they are not relative to anything else and are generally considered to always be the same size.

| Unit | Name                | Equivalent to       |
| ---- | ------------------- | ------------------- |
| `cm` | Centimeters         | 1cm = 96px/2.54     |
| `mm` | Millimeters         | 1mm = 1/10th of 1cm |
| `Q`  | Quarter-millimeters | 1Q = 1/40th of 1cm  |
| `in` | Inches              | 1in = 2.54cm = 96px |
| `pc` | Picas               | 1pc = 1/6th of 1in  |
| `pt` | Points              | 1pt = 1/72th of 1in |
| `px` | Pixels              | 1px = 1/96th of 1in |

**Relative length units**

Relative length units are relative to something else, perhaps the size of the parent element's font, or the size of the viewport. The benefit of using relative units is that with some careful planning you can make it so the size of text or other elements scale relative to everything else on the page.

| Unit   | Relative to                                                                                                                                                                                                                                                                                   |
| ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `em`   | Font size of the parent, in the case of typographical properties like [`font-size`](https://developer.mozilla.org/en-US/docs/Web/CSS/font-size), and font size of the element itself, in the case of other properties like [`width`](https://developer.mozilla.org/en-US/docs/Web/CSS/width). |
| `ex`   | x-height of the element's font.                                                                                                                                                                                                                                                               |
| `ch`   | The advance measure (width) of the glyph "0" of the element's font.                                                                                                                                                                                                                           |
| `rem`  | Font size of the root element.                                                                                                                                                                                                                                                                |
| `lh`   | Line height of the element.                                                                                                                                                                                                                                                                   |
| `vw`   | 1% of the viewport's width.                                                                                                                                                                                                                                                                   |
| `vh`   | 1% of the viewport's height.                                                                                                                                                                                                                                                                  |
| `vmin` | 1% of the viewport's smaller dimension.                                                                                                                                                                                                                                                       |
| `vmax` | 1% of the viewport's larger dimension.                                                                                                                                                                                                                                                        |

## How to select elements via attribute name and content?

The CSS **attribute selector** matches elements based on the presence or value of a given attribute.

```css
/* <a> elements with a title attribute */
a[title] {
  color: purple;
}

/* <a> elements with an href matching "https://example.org" */
a[href="https://example.org"] {
  color: green;
}

/* <a> elements with an href containing "example" */
a[href*="example"] {
  font-size: 2em;
}

/* <a> elements with an href ending ".org" */
a[href$=".org"] {
  font-style: italic;
}

/* <a> elements whose class attribute contains the word "logo" */
a[class~="logo"] {
  padding: 2px;
}
```

## How to apply multiple selectors to the same rule?

To group CSS selectors in a style sheet, [use commas to separate multiple grouped selectors](https://www.lifewire.com/comma-in-css-selectors-3467052) in the style. In this example, the style affects the p and div elements:

```css
div, p { color: #f00; }
```

In this context, a comma means "and," so this selector applies to all paragraph elements and all division elements. If the comma were missing, the selector would instead apply to all paragraph elements that are a child of a division. That is a different kind of selector, so the comma is important.

## How do we make a rounded corner by using CSS?

We can make a rounded corner by using the property “border-radius”. We can apply this property to any element.

## What's the difference between `inline` and `inline-block`?

I shall throw in a comparison with `block` for good measure.

|                                      | `block`                                                                                     | `inline-block`                                                      | `inline`                                                                                                                                                                                                             |
| ------------------------------------ | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Size                                 | Fills up the width of its parent container.                                                 | Depends on content.                                                 | Depends on content.                                                                                                                                                                                                  |
| Positioning                          | Start on a new line and tolerates no HTML elements next to it (except when you add `float`) | Flows along with other content and allows other elements beside it. | Flows along with other content and allows other elements beside it.                                                                                                                                                  |
| Can specify `width` and `height`     | Yes                                                                                         | Yes                                                                 | No. Will ignore if being set.                                                                                                                                                                                        |
| Can be aligned with `vertical-align` | No                                                                                          | Yes                                                                 | Yes                                                                                                                                                                                                                  |
| Margins and paddings                 | All sides respected.                                                                        | All sides respected.                                                | Only horizontal sides respected. Vertical sides, if specified, do not affect layout. Vertical space it takes up depends on `line-height`, even though the `border` and `padding` appear visually around the content. |
| Float                                | -                                                                                           | -                                                                   | Becomes like a `block` element where you can set vertical margins and paddings.                                                                                                                                      |

## What is the CSS `display` property and can you give a few examples of its use?

* `none`, `block`, `inline`, `inline-block`, `flex`, `grid`, `table`, `table-row`, `table-cell`, `list-item`.

| `display`      | Description                                                                                                                                                                                                            |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `none`         | Does not display an element (the elements no longer affects the layout of the document). All child element are also no longer displayed. The document is rendered as if the element did not exist in the document tree |
| `block`        | The element consumes the whole line in the block direction (which is usually horizontal)                                                                                                                               |
| `inline`       | Elements can be laid out beside each other                                                                                                                                                                             |
| `inline-block` | Similar to `inline`, but allows some `block` properties like setting `width` and `height`                                                                                                                              |
| `table`        | Behaves like the `<table>` element                                                                                                                                                                                     |
| `table-row`    | Behaves like the `<tr>` element                                                                                                                                                                                        |
| `table-cell`   | Behaves like the `<td>` element                                                                                                                                                                                        |
| `list-item`    | Behaves like a `<li>` element which allows it to define `list-style-type` and `list-style-position`                                                                                                                    |

## What's the difference between a `relative`, `fixed`, `absolute` and `static`ally positioned element?

A positioned element is an element whose computed `position` property is either `relative`, `absolute`, `fixed` or `sticky`.

* `static` - The default position; the element will flow into the page as it normally would. The `top`, `right`, `bottom`, `left` and `z-index` properties do not apply.
* `relative` - The element's position is adjusted relative to itself, without changing layout (and thus leaving a gap for the element where it would have been had it not been positioned).
* `absolute` - The element is removed from the flow of the page and positioned at a specified position relative to its closest positioned ancestor if any, or otherwise relative to the initial containing block. Absolutely positioned boxes can have margins, and they do not collapse with any other margins. These elements do not affect the position of other elements.
* `fixed` - The element is removed from the flow of the page and positioned at a specified position relative to the viewport and doesn't move when scrolled.
* `sticky` - Sticky positioning is a hybrid of relative and fixed positioning. The element is treated as `relative` positioned until it crosses a specified threshold, at which point it is treated as `fixed` positioned.

## How to control overflowing content?

Everything in CSS is a box. It can constrain the size of these boxes by assigning values of [`width`](https://developer.mozilla.org/en-US/docs/Web/CSS/width) and [`height`](https://developer.mozilla.org/en-US/docs/Web/CSS/height) (or [`inline-size`](https://developer.mozilla.org/en-US/docs/Web/CSS/inline-size) and [`block-size`](https://developer.mozilla.org/en-US/docs/Web/CSS/block-size)). **Overflow happens when there is too much content to fit in a box.** CSS provides various tools to manage overflow. As this go further with CSS layout and writing CSS, it will encounter more overflow situations.

```css
.box {
  border: 1px solid #333333;
  width: 200px;
  height: 100px;
  overflow: auto;
}
```

{% embed url="https://developer.mozilla.org/en-US/docs/Web/CSS/text-overflow" %}
