# Responsive Design

## Can you give an example of an @media property other than screen?

Yes, there are four types of @media properties (including _screen_):

* `all` - for all media type devices
* `print` - for printers
* `speech` - for screenreaders that "reads" the page out loud
* `screen` - for computer screens, tablets, smart-phones etc.

Here is an example of `print` media type's usage:

```css
@media print {
  body {
    color: black;
  }
}
```

## Have you ever used a grid system, and if so, what do you prefer?

Before Flex became popular (around 2014), the `float`-based grid system was the most reliable because it still has the most browser support among the alternative existing systems (flex, grid). Bootstrap was using the `float` approach until Bootstrap 4 which switched to the `flex`-based approach. As of writing (2020), `flex` is the recommended approach for building grid systems and has [decent browser support](https://caniuse.com/#search=flex).

For the adventurous, they can look into [CSS Grid Layout](https://css-tricks.com/snippets/css/complete-guide-grid/), which uses the shiny new `grid` property; it is even better than `flex` for building grid layouts and will be the de facto way to do so in the future.

## Have you used or implemented media queries or mobile-specific layouts/CSS?

Yes. An example would be transforming a stacked pill navigation into a fixed-bottom tab navigation beyond a certain breakpoint.\


#### Can you explain the difference between coding a website to be responsive versus using a mobile-first strategy?

Note that these two 2 approaches are not exclusive.

Making a website responsive means the some elements will respond by adapting its size or other functionality according to the device's screen size, typically the viewport width, through CSS media queries, for example, making the font size smaller on smaller devices.

```css
@media (min-width: 601px) {
  .my-class {
    font-size: 24px;
  }
}

@media (max-width: 600px) {
  .my-class {
    font-size: 12px;
  }
}
```

A mobile-first strategy is also responsive, however it agrees we should default and define all the styles for mobile devices, and only add specific responsive rules to other devices later. Following the previous example:

```css
.my-class {
  font-size: 12px;
}

@media (min-width: 600px) {
  .my-class {
    font-size: 24px;
  }
}
```

A mobile-first strategy has 2 main advantages:

* It's more performant on mobile devices, since all the rules applied for them don't have to be validated against any media queries.
* It forces to write cleaner code in respect to responsive CSS rules.

## How is responsive design different from adaptive design?

Both responsive and adaptive design attempt to optimize the user experience across different devices, adjusting for different viewport sizes, resolutions, usage contexts, control mechanisms, and so on.

Responsive design works on the principle of flexibility - a single fluid website that can look good on any device. Responsive websites use media queries, flexible grids, and responsive images to create a user experience that flexes and changes based on a multitude of factors. Like a single ball growing or shrinking to fit through several different hoops.

Adaptive design is more like the modern definition of progressive enhancement. Instead of one flexible design, adaptive design detects the device and other features and then provides the appropriate feature and layout based on a predefined set of viewport sizes and other characteristics. The site detects the type of device used and delivers the pre-set layout for that device. Instead of a single ball going through several different-sized hoops, you'd have several different balls to use depending on the hoop size.

Both have these methods have some issues that need to be weighed:

* Responsive design can be quite challenging, as you're essentially using a single albeit responsive layout to fit all situations. How to set the media query breakpoints is one such challenge. Do you use standardized breakpoint values? Or, do you use breakpoints that make sense to your particular layout? What if that layout changes?
* Adaptive design generally requires user agent sniffing, or DPI detection, etc., all of which can prove unreliable.
