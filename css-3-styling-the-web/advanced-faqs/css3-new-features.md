# CSS3 New features

## What are new features in CSS3?

#### Box Shadow <a href="#box-shadow" id="box-shadow"></a>

One of the CSS3 new features is the [box-shadow](https://www.bitdegree.org/learn/css-box-shadow) property that adds a shadow to an element. Instead of using multiple images around an item, this property lets you add shadow with a short line of code.

#### Opacity <a href="#opacity" id="opacity"></a>

One of the CSS3 properties called [opacity](https://www.bitdegree.org/learn/css-transparency) makes elements **see-through** or completely **transparent**.

For instance, you can apply `opacity` to images or other HTML elements. The transparency level depends on the **indicated values.**

#### Rounded Corners <a href="#rounded-corners" id="rounded-corners"></a>

Before the release of CSS3, developers had to write long code to produce rounded corners. Now, it is enough to apply the [border-radius](https://www.bitdegree.org/learn/css-border-radius) CSS3 property to HTML elements.

#### Attribute Selectors <a href="#attribute-selectors" id="attribute-selectors"></a>

CSS3 also introduced new [selectors](https://www.bitdegree.org/learn/css-syntax) in addition to the ones in CSS2. Instead of applying **IDs** or **classes** for styling, developers can select HTML elements according to their **attributes**.

As a result, you do not have to create unique IDs only to apply CSS rules.

#### New Colors <a href="#new-colors" id="new-colors"></a>

One of the CSS3 features is the addition of new [colors](https://www.bitdegree.org/learn/css-colors):

* RGBA
* HSL
* HSLA
* Gradient Colors

#### Web-Safe Fonts <a href="#more-than-web-safe-fonts" id="more-than-web-safe-fonts"></a>

Instead of only using [fonts](https://www.bitdegree.org/learn/css-font) labeled as **web-safe**, developers now can apply more unique fonts in their HTML documents. Before that, CSS wanted to ensure that all browsers and machines display fonts the same.

## Is there any reason you'd want to use `translate()` instead of `absolute` positioning, or vice-versa? And why?

`translate()` is a value of CSS `transform`. Changing `transform` or `opacity` does not trigger browser reflow or repaint but does trigger compositions; whereas changing the absolute positioning triggers `reflow`. `transform` causes the browser to create a GPU layer for the element but changing absolute positioning properties uses the CPU. Hence `translate()` is more efficient and will result in shorter paint times for smoother animations.

When using `translate()`, the element still occupies its original space (sort of like `position: relative`), unlike in changing the absolute positioning.

## **What are gradients in CSS?**

* Linear Gradient
* Radial Gradient

There are two types of gradients that are present in CSS. **They are:**

**Answer:** It is a property of CSS which allows you to display a smooth transformation between two or more than two specified colors.

\
