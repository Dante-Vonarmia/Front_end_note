# Cascade and inheritance

## Basic Concept

### Cascade

The cascade Stylesheets cascade — at a very simple level this means that the order of CSS rules matter; when two rules apply that have equal specificity the one that comes last in the CSS is the one that will be used.

### Inheritance

Inheritance also needs to be understood in this context — some CSS property values set on parent elements are inherited by their child elements, and some aren't.&#x20;

For example if you set a width of 50% on an element, all of its descendants do not get a width of 50% of their parent's width. If this was the case, CSS would be very frustrating to use!

### Specificity

Specificity is how the browser decides which rule applies if multiple rules have different selectors, but could still apply to the same element. It is basically a measure of how specific a selector's selection will be:

* An element selector is less specific — it will select all elements of that type that appear on a page — so will get a lower score.&#x20;
* A class selector is more specific — it will select only the elements on a page that have a specific class attribute value — so will get a higher score.

## Explain what is CSS selector specificity and how does it work?

The browser determines what styles to show on an element depending on the specificity of CSS rules. We assume that the browser has already determined the rules that match a particular element. Among the matching rules, the specificity, four comma-separate values, `a, b, c, d` are calculated for each rule based on the following:

1. `a` is whether inline styles are being used. If the property declaration is an inline style on the element, `a` is 1, else 0.
2. `b` is the number of ID selectors.
3. `c` is the number of classes, attributes and pseudo-classes selectors.
4. `d` is the number of tags and pseudo-elements selectors.

The resulting specificity is not a score, but a matrix of values that can be compared column by column. When comparing selectors to determine which has the highest specificity, look from left to right, and compare the highest value in each column. So a value in column `b` will override values in columns `c` and `d`, no matter what they might be. As such, specificity of `0,1,0,0` would be greater than one of `0,0,10,10`.

In the cases of equal specificity: the latest rule is the one that counts. If you have written the same rule into your stylesheet (regardless of internal or external) twice, then the lower rule in your style sheet is closer to the element to be styled, it is deemed to be more specific and therefore will be applied.

I would write CSS rules with low specificity so that they can be easily overridden if necessary. When writing CSS UI component library code, it is important that they have low specificities so that users of the library can override them without using too complicated CSS rules just for the sake of increasing specificity or resorting to `!important`.

## How to calculate specificity of a CSS selector?

Thousands: Score one in this column if the declaration is inside a style attribute, aka inline styles. Such declarations don't have selectors, so their specificity is always simply 1000.

Hundreds: Score one in this column for each ID selector contained inside the overall selector.

Tens: Score one in this column for each class selector, attribute selector, or pseudo-class contained inside the overall selector.

Ones: Score one in this column for each element selector or pseudo-element contained inside the overall selector.

## How to control inheritance in CSS?

Inheritance also needs to be understood in this context — some CSS property values set on parent elements are inherited by their child elements, and some aren't.

For example if you set a width of 50% on an element, all of its descendants do not get a width of 50% of their parent's width. If this was the case, CSS would be very frustrating to use!

## How do I restore the default value of a property?

#### initial

Sets the property value applied to a selected element to the initial value of that property.

#### unset&#x20;

Resets the property to its natural value, which means that if the property is naturally inherited it acts like inherit, otherwise it acts like initial.

## How do I derive one style from another?

#### inherit&#x20;

Sets the property value applied to a selected element to be the same as that of its parent element. Effectively, this "turns on inheritance".
