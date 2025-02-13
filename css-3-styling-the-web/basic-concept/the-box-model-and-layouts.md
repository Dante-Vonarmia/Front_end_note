# The box model and Layouts

## Explain your understanding of the box model and how you would tell the browser in CSS to render your layout in different box models.

The CSS box model describes the rectangular boxes that are generated for elements in the document tree and laid out according to the visual formatting model. Each box has a content area (e.g. text, an image, etc.) and optional surrounding `padding`, `border`, and `margin` areas.

The CSS box model is responsible for calculating:

* How much space a block element takes up.
* Whether or not borders and/or margins overlap, or collapse.
* A box's dimensions.

The box model has the following rules:

* The dimensions of a block element are calculated by `width`, `height`, `padding`, `border`s, and `margin`s.
* If no `height` is specified, a block element will be as high as the content it contains, plus `padding` (unless there are floats, for which see below).
* If no `width` is specified, a non-floated block element will expand to fit the width of its parent minus `padding`.
* The `height` of an element is calculated by the content's `height`.
* The `width` of an element is calculated by the content's `width`.
* By default, `padding`s and `border`s are not part of the `width` and `height` of an element.

## Describe `float` and how they work.

Float is a CSS positioning property. Floated elements remain a part of the flow of the page, and will affect the positioning of other elements (e.g. text will flow around floated elements), unlike `position: absolute` elements, which are removed from the flow of the page.

The CSS `clear` property can be used to be positioned below `left`/`right`/`both` floated elements.

If a parent element contains nothing but floated elements, its height will be collapsed to nothing. It can be fixed by clearing the float after the floated elements in the container but before the close of the container.

The `.clearfix` hack uses a clever CSS [pseudo selector](https://github.com/yangshun/front-end-interview-handbook/blob/master/contents/en/css-questions.md#describe-pseudo-elements-and-discuss-what-they-are-used-for) (`:after`) to clear floats. Rather than setting the overflow on the parent, you apply an additional class `clearfix` to it. Then apply this CSS:

```css
.clearfix:after {
  content: ' ';
  visibility: hidden;
  display: block;
  height: 0;
  clear: both;
}
```

Alternatively, give `overflow: auto` or `overflow: hidden` property to the parent element which will establish a new block formatting context inside the children and it will expand to contain its children.

## Describe `z-index` and how stacking context is formed.

The `z-index` property in CSS controls the vertical stacking order of elements that overlap. `z-index` only affects elements that have a `position` value which is not `static`.

Without any `z-index` value, elements stack in the order that they appear in the DOM (the lowest one down at the same hierarchy level appears on top). Elements with non-static positioning (and their children) will always appear on top of elements with default static positioning, regardless of HTML hierarchy.

A stacking context is an element that contains a set of layers. Within a local stacking context, the `z-index` values of its children are set relative to that element rather than to the document root. Layers outside of that context — i.e. sibling elements of a local stacking context — can't sit between layers within it. If an element B sits on top of element A, a child element of element A, element C, can never be higher than element B even if element C has a higher `z-index` than element B.

Each stacking context is self-contained - after the element's contents are stacked, the whole element is considered in the stacking order of the parent stacking context. A handful of CSS properties trigger a new stacking context, such as `opacity` less than 1, `filter` that is not `none`, and `transform` that is not`none`.

_Note: What exactly qualifies an element to create a stacking context is listed in this long set of_ [_rules_](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context#The_stacking_context)_._

## Have you played around with the new CSS Flexbox or Grid specs?

Yes. Flexbox is mainly meant for 1-dimensional layouts while Grid is meant for 2-dimensional layouts.

Flexbox solves many common problems in CSS, such as vertical centering of elements within a container, sticky footer, etc. Bootstrap and Bulma are based on Flexbox, and it is probably the recommended way to create layouts these days. Have tried Flexbox before but ran into some browser incompatibility issues (Safari) in using `flex-grow`, and I had to rewrite my code using `inline-blocks` and math to calculate the widths in percentages, it wasn't a nice experience.

Grid is by far the most intuitive approach for creating grid-based layouts (it better be!) but browser support is not wide at the moment.

## How many ways to make an elements's position is center to its parent elements?

#### Text-Align Metho&#x64;**:**

1. Enclose the div that you want to center with a parent element (commonly known as a wrapper or container)
2. Set “text-align: center” to parent element
3. Then set the inside div to “display: inline-block”

#### Margin Auto Method:

1. Don’t need a parent element.
2. By simply apply “margin: 0 auto” to our box, as long as we have a defined width.

#### Absolute Positioning Method <a href="#absolute-positioning-method" id="absolute-positioning-method"></a>

> This method can cause overlapping of elements if used incorrectly.

1. Set the element’s position property to absolute
2. Apply “left: 50%” to the element
3. Set a margin-left of half of the element’s width

#### Transform/Translate Method <a href="#transform-translate-method" id="transform-translate-method"></a>

This method is used frequently in responsive design and doesn’t require margins to be defined, like in the absolute positioning method.

#### Flex-box Method

The four steps to centering horizontally and vertically with Flex-box are the following:

1. HTML, body, and parent container need to have a height of 100%
2. Set display to flex on parent container
3. Set align-items to center on parent container
4. Set justify-content to center on parent container

{% hint style="info" %}
I like using this method because it’s both **responsive** and **doesn’t require any margin calculations**.
{% endhint %}

{% embed url="https://www.freecodecamp.org/news/how-to-center-things-with-style-in-css-dc87b7542689/" %}
Check this article for more details
{% endembed %}

## Give a sample of align-center / Give a sample of vertical align center. (Both block and inline elements)

{% embed url="https://css-tricks.com/centering-css-complete-guide/" %}
Check this article for more details
{% endembed %}

## What's the difference between `margin` and `padding`?

In CSS, the margin is the property by which we can create space around elements. We can even create space to the exterior defined borders.

**In CSS, we have margin property as follows:**

* margin-top
* margin-right
* margin-bottom
* Margin-left

**Margin property has some defined values as shown below.**

* **Auto –** Using this property browser calculates the margin.
* **Length –** It sets the margin values in px,pt,cm etc.
* **% –** It sets the width % of the element.
* **Inherit –** By this property we can inherit the margin property from the parent element.

In CSS, padding is the property by which we can generate space around an element’s content as well as inside any known border.

**CSS padding also has properties like,**

1. Padding-top
2. Padding-right
3. Padding-bottom
4. Padding-left

Negative values are not allowed in padding.

## Explain `margin` collapse?

The [top](https://developer.mozilla.org/en-US/docs/Web/CSS/margin-top) and [bottom](https://developer.mozilla.org/en-US/docs/Web/CSS/margin-bottom) margins of blocks are sometimes combined (collapsed) into a single margin whose size is the largest of the individual margins (or just one of them, if they are equal), a behavior known as **margin collapsing**. Note that the margins of [floating](https://developer.mozilla.org/en-US/docs/Web/CSS/float) and [absolutely positioned](https://developer.mozilla.org/en-US/docs/Web/CSS/position#absolute) elements never collapse.

Margin collapsing occurs in three basic cases:

#### Adjacent siblings

The margins of adjacent siblings are collapsed (except when the latter sibling needs to be [cleared](https://developer.mozilla.org/en-US/docs/Web/CSS/clear) past floats).

#### No content separating parent and descendants

If there is no border, padding, inline part, [block formatting context](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Block_formatting_context) created, or [_clearance_](https://developer.mozilla.org/en-US/docs/Web/CSS/clear) to separate the [`margin-top`](https://developer.mozilla.org/en-US/docs/Web/CSS/margin-top) of a block from the [`margin-top`](https://developer.mozilla.org/en-US/docs/Web/CSS/margin-top) of one or more of its descendant blocks; or no border, padding, inline content, [`height`](https://developer.mozilla.org/en-US/docs/Web/CSS/height), [`min-height`](https://developer.mozilla.org/en-US/docs/Web/CSS/min-height), or [`max-height`](https://developer.mozilla.org/en-US/docs/Web/CSS/max-height) to separate the [`margin-bottom`](https://developer.mozilla.org/en-US/docs/Web/CSS/margin-bottom) of a block from the [`margin-bottom`](https://developer.mozilla.org/en-US/docs/Web/CSS/margin-bottom) of one or more of its descendant blocks, then those margins collapse. The collapsed margin ends up outside the parent.

#### Empty blocks

If there is no border, padding, inline content, [`height`](https://developer.mozilla.org/en-US/docs/Web/CSS/height), or [`min-height`](https://developer.mozilla.org/en-US/docs/Web/CSS/min-height) to separate a block's [`margin-top`](https://developer.mozilla.org/en-US/docs/Web/CSS/margin-top) from its [`margin-bottom`](https://developer.mozilla.org/en-US/docs/Web/CSS/margin-bottom), then its top and bottom margins collapse.

Some things to note:

* More complex margin collapsing (of more than two margins) occurs when the above cases are combined.
* These rules apply even to margins that are zero, so the margin of a descendant ends up outside its parent (according to the rules above) whether or not the parent's margin is zero.
* When negative margins are involved, the size of the collapsed margin is the sum of the largest positive margin and the smallest (most negative) negative margin.
* When all margins are negative, the size of the collapsed margin is the smallest (most negative) margin. This applies to both adjacent elements and nested elements.

## `position` , all value, when and why? (hint: DOM flow)

* `static`: every element has a static position by default, so the element will stick to the normal page flow. So if there is a [left](https://css-tricks.com/almanac/properties/l/left/)/[right](https://css-tricks.com/almanac/properties/r/right/)/[top](https://css-tricks.com/almanac/properties/t/top/)/[bottom](https://css-tricks.com/almanac/properties/b/bottom/)/[z-index](https://css-tricks.com/almanac/properties/z/z-index/) set then there will be no effect on that element.
* `relative`: an element’s original position remains in the flow of the document, just like the `static` value. But now [left](https://css-tricks.com/almanac/properties/l/left/)/[right](https://css-tricks.com/almanac/properties/r/right/)/[top](https://css-tricks.com/almanac/properties/t/top/)/[bottom](https://css-tricks.com/almanac/properties/b/bottom/)/[z-index](https://css-tricks.com/almanac/properties/z/z-index/) will work. The positional properties “nudge” the element from the original position in that direction.
* `absolute`: the element is removed from the flow of the document and other elements will behave as if it’s not even there whilst all the other positional properties will work on it.
* `fixed`: the element is removed from the flow of the document like absolutely positioned elements. In fact they behave almost the same, only fixed positioned elements are always relative to the document, not any particular parent, and are unaffected by scrolling.
* `sticky` (experimental): the element is treated like a `relative` value until the scroll location of the viewport reaches a specified threshold, at which point the element takes a `fixed` position where it is told to stick.
* `inherit`: the `position` value doesn’t cascade, so this can be used to specifically force it to, and `inherit` the positioning value from its parent.

## What are the common properties to size item, for example min or max size?

#### Width Properties

The first thing to discuss is width-related properties. We have `min-width` and `max-width`, and each one of them is important and has its use cases.

#### Min Width <a href="#min-width" id="min-width"></a>

When setting the value of `min-width`, its benefit lies in preventing the used value for `width` property from becoming less than the specified value for `min-width`. Note that the default value for `min-width` is `auto`, which resolves to `0`.

#### Max Width <a href="#max-width" id="max-width"></a>

When setting the value of `max-width`, its benefit lies in preventing the used value for `width` property from becoming more than the specified value for `max-width`. \
The default value for `max-width` is `none`.

#### Height Properties

In addition to the minimum and maximum width properties, we have the same properties as the height.

#### Min Height <a href="#min-height" id="min-height"></a>

When setting the value of `min-height`, its benefit lies in preventing the used value for `height` property from becoming less than the specified value for `min-height`. Note that the default value for `min-height` is `auto`, which resolves to `0`.

#### Max Height <a href="#max-height" id="max-height"></a>

When setting the value of max-height, its benefit lies in preventing the used value for height property from becoming more than the specified value for max-height. Note that the default value for max-height is none.

Consider the below example where I set max-height for the content. But, because it’s bigger than the specified space, there is an overflow. The text is out of its parent boundaries due to that.

## How to control the part of a CSS box that the background is drawn under?

The **`background-image`** [CSS](https://developer.mozilla.org/en-US/docs/Web/CSS) property sets one or more background images on an element.

The background images are drawn on stacking context layers on top of each other. The first layer specified is drawn as if it is closest to the user.

## How to use background-clip to control how much of the box your background image covers?

The **`background-clip`** CSS property sets whether an element's background extends underneath its border box, padding box, or content box.

If the element has no [`background-image`](https://developer.mozilla.org/en-US/docs/Web/CSS/background-image) or [`background-color`](https://developer.mozilla.org/en-US/docs/Web/CSS/background-color), this property will only have a visual effect when the border has transparent regions or partially opaque regions (due to [`border-style`](https://developer.mozilla.org/en-US/docs/Web/CSS/border-style) or [`border-image`](https://developer.mozilla.org/en-US/docs/Web/CSS/border-image)); otherwise, the border masks the difference.\


## What does `* { box-sizing: border-box; }` do? What are its advantages?

* By default, elements have `box-sizing: content-box` applied, and only the content size is being accounted for.
* `box-sizing: border-box` changes how the `width` and `height` of elements are being calculated, `border` and `padding` are also being included in the calculation.
* The `height` of an element is now calculated by the content's `height` + vertical `padding` + vertical `border` width.
* The `width` of an element is now calculated by the content's `width` + horizontal `padding` + horizontal `border` width.
* Taking into account `padding`s and `border`s as part of our box model resonates better with how designers actually imagine content in grids.

## How to add shadows to boxes?

Used in casting shadows off block-level elements (like divs).

```css
.shadow {
  -moz-box-shadow:    3px 3px 5px 6px #ccc;
  -webkit-box-shadow: 3px 3px 5px 6px #ccc;
  box-shadow:         3px 3px 5px 6px #ccc;
}
```

1. **The horizontal offset** of the shadow, positive means the shadow will be on the right of the box, a negative offset will put the shadow on the left of the box.
2. **The vertical offset** of the shadow, a negative one means the box-shadow will be above the box, a positive one means the shadow will be below the box.
3. **The blur radius** (optional), if set to 0 the shadow will be sharp, the higher the number, the more blurred it will be.
4. **The spread radius** (optional), positive values increase the size of the shadow, negative values decrease the size. Default is 0 (the shadow is same size as blur).
5. **Color**

## Using CSS flexible boxes

**CSS Flexible Box Layout** is a module of [CSS](https://developer.mozilla.org/en-US/docs/Web/CSS) that defines a CSS box model optimized for user interface design, and the layout of items in one dimension. In the flex layout model, the children of a flex container can be laid out in any direction, and can “flex” their sizes, either growing to fill unused space or shrinking to avoid overflowing the parent. Both horizontal and vertical alignment of the children can be easily manipulated.

## Using CSS multi-column layouts

The **CSS Multi-column Layout Module** extends the _block layout mode_ to allow the easy definition of multiple columns of text. People have trouble reading text if lines are too long; if it takes too long for the eyes to move from the end of the one line to the beginning of the next, they lose track of which line they were on. Therefore, to make maximum use of a large screen, authors should have limited-width columns of text placed side by side, just as newspapers do.

Unfortunately this is impossible to do with CSS and HTML without forcing column breaks at fixed positions, or severely restricting the markup allowed in the text, or using heroic scripting. This limitation is solved by adding new CSS properties to extend the traditional block layout mode.

## Using CSS generated content

One of the important advantages of CSS is that it helps you to separate a document's style from its content. However, there are situations where it makes sense to specify certain content as part of the stylesheet, not as part of the document. You can specify text or image content within a stylesheet when that content is closely linked to the document's structure.&#x20;

{% hint style="info" %}
Content specified in a stylesheet does not become part of the DOM.
{% endhint %}

#### Text content <a href="#text_content" id="text_content"></a>

CSS can insert text content before or after an element. To specify this, make a rule and add [`::before`](https://developer.mozilla.org/en-US/docs/Web/CSS/::before) or [`::after`](https://developer.mozilla.org/en-US/docs/Web/CSS/::after) to the selector. In the declaration, specify the [`content`](https://developer.mozilla.org/en-US/docs/Web/CSS/content) property with the text content as its value.

#### Image content

To add an image before or after an element, you can specify the URL of an image file in the value of the [`content`](https://developer.mozilla.org/en-US/docs/Web/CSS/content) property.

## Useful Layout Solution

{% embed url="https://web.dev/one-line-layouts/" %}
