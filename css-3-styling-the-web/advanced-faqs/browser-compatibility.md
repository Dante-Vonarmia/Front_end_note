# Browser Compatibility

## What do the -moz-\*, -ms-\*, -webkit-\*, -o-\* and -khtml-\* properties do?

These properties, called _prefixed properties_, are extensions to the CSS standard. They allow use of experimental and non-standard features in browsers without polluting the regular namespace, preventing future incompatibilities to arise when the standard is extended.

The use of such properties on production websites is not recommended — they have already created a huge web compatibility mess. For example, many developers only using the `-webkit-` prefixed version of a property when the non-prefixed version is supported across all browsers meant that a feature relying on that property would break in non-webkit-based browsers, completely needlessly. This problem got so bad that other browsers started to implement `-webkit-` prefixed aliases to improve web compatibility, as specified in the [Compatibility Living Standard](https://compat.spec.whatwg.org/).

In fact most browsers now do not use CSS prefixes when implementing experimental features, instead implementing those features only on Nightly browser versions or similar.

If you need to use prefixes in your work, you are advised to write your code in a way that uses the prefixed versions first, but then includes a non-prefixed standard version afterwards so it can automatically override the prefixed versions where supported. For example:

```css
-ms-transform: rotate(90deg);
-webkit-transform: rotate(90deg);
transform: rotate(90deg);
```

## How to check and supporting older browsers?

{% hint style="info" %}
[caniuse.com ](https://caniuse.com)is the most common tool to test whether your browser support the feature or not.
{% endhint %}

There’s a better way: You can check whether a feature exists. If it exists, use it. If not, provide fallback code.

**Deciding whether to use a feature**

**Deciding what browsers to support**

**The level of support**

1. everything must look and work the same in all browsers
2. the site must look the same, but functionality can be different across browsers
3. functionality must be the same, but looks can be different across browsers
4. looks and functionality can both differ across browsers

**Wrapping up**

Think about it:

1. why are you trying to support the old browser you’re trying to support?
2. what level of support are you giving?
3. is it worth the resources you’ve allocated?

#### Supporting Older Browsers — CSS <a href="#supporting-older-browsers-css" id="supporting-older-browsers-css"></a>

There are two ways to provide fallbacks for CSS features:

1. property fallbacks
2. feature queries

**Property fallbacks**

{% hint style="info" %}
If a browser doesn’t recognize a property or its corresponding value, the browser will ignore the property altogether.
{% endhint %}

When this happens, the browser uses — or falls back — to the previous value it finds.

This is the easiest way to provide a fallback.

Here’s an example:

```css
.layout {  display: block;   display: grid; }
```

In this example, browsers that support CSS Grid will use `display: grid`. A browser that doesn’t support CSS Grid will fall back to `display: block`.

{% embed url="https://www.freecodecamp.org/news/why-you-should-care-about-supporting-older-browsers-39bbc28fb7fd/" %}
Check this for more detail
{% endembed %}

## Have you ever worked with retina graphics? If so, when and what techniques did you use?

_Retina_ is just a marketing term to refer to high resolution screens with a pixel ratio bigger than 1. The key thing to know is that using a pixel ratio means these displays are emulating a lower resolution screen in order to show elements with the same size. Nowadays we consider all mobile devices _retina_ defacto displays.

Browsers by default render DOM elements according to the device resolution, except for images.

In order to have crisp, good-looking graphics that make the best of retina displays we need to use high resolution images whenever possible. However using always the highest resolution images will have an impact on performance as more bytes will need to be sent over the wire.

To overcome this problem, we can use responsive images, as specified in HTML5. It requires making available different resolution files of the same image to the browser and let it decide which image is best, using the html attribute `srcset` and optionally `sizes`, for instance:

```markup
<div responsive-background-image>
  <img
    src="/images/test-1600.jpg"
    sizes="
      (min-width: 768px) 50vw,
      (min-width: 1024px) 66vw,
      100vw"
    srcset="
      /images/test-400.jpg   400w,
      /images/test-800.jpg   800w,
      /images/test-1200.jpg 1200w
    "
  />
</div>
```

It is important to note that browsers which don't support HTML5's `srcset` (i.e. IE11) will ignore it and use `src` instead. If we really need to support IE11 and we want to provide this feature for performance reasons, we can use a JavaScript polyfill, e.g. Picturefill (link in the references).

For icons, I would also opt to use SVGs and icon fonts where possible, as they render very crisply regardless of resolution.

## How do you serve your pages for feature-constrained browsers? What techniques/processes do you use?

* Graceful degradation - The practice of building an application for modern browsers while ensuring it remains functional in older browsers.
* Progressive enhancement - The practice of building an application for a base level of user experience, but adding functional enhancements when a browser supports it.
* Use [caniuse.com](https://caniuse.com/) to check for feature support.
* Autoprefixer for automatic vendor prefix insertion.
* Feature detection using [Modernizr](https://modernizr.com/).
* Use CSS Feature queries [@support](https://developer.mozilla.org/en-US/docs/Web/CSS/@supports)

## How would you approach fixing browser-specific styling issues?

* After identifying the issue and the offending browser, use a separate style sheet that only loads when that specific browser is being used. This technique requires server-side rendering though.
* Use libraries like Bootstrap that already handles these styling issues for you.
* Use `autoprefixer` to automatically add vendor prefixes to your code.
* Use Reset CSS or Normalize.css.
* If you're using Postcss (or a similar transpiling library), there may be plugins which allow you to opt in for using modern CSS syntax (and even W3C proposals) that will transform those sections of your code into corresponding safe code that will work in the targets you've used.
