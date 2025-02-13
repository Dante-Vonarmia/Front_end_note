# Performance & SEO

## Website Performance Rules

* Rule 1: Make Fewer HTTP Requests
* Rule 2: Use a Content Delivery Network
* Rule 3: Add an Expires Header
* Rule 4: Gzip Components
* Rule 5: Put Stylesheets at the Top
* Rule 6: Put Scripts at the Bottom
* Rule 7: Avoid CSS Expressions
* Rule 8: Make JavaScript and CSS External
* Rule 9: Reduce DNS Lookups
* Rule 10: Minify JavaScript
* Rule 11: Avoid Redirects
* Rule 12: Remove Duplicate Scripts

## What will happened if you don't add DOCTYPE for HTML5

The foremost thing that you need to make sure is that have you added the DOCTYPE in your HTML file.

Doctype basically helps your browser to recognize in which language is your website’s code written. If you don’t specify that, some of the smart browsers will understand it themselves but some dumb browser will not be able to figure out what happened, and they will render some element of your website in a way that you would not like.

So, if you want that IE6 and above should imitate the behavior of browser like chrome and Firefox you may want to add a `strict doctype`.

```markup
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN""http://www.w3.org/TR/html4/strict.dtd">
```

If you don’t do that, the browser will work in `Quirks mode` and will emulate the behavior of older versions.

## What is the advantage of collapsing white space?

It is always good habits to follow a clean code guide not only for yourself, but also for the whole team and future developer.

A proper collapsing white space will make your HTML structure tree simply easier to read and more reasonable. It's a basic routine to always check your own HTML structure trees.

## Common cross browser compatibility issues.

#### Find cross browser compatibility issues with Opera Mini Mobile Browser:

If you are using elements like

* CSS3 3D Transforms
* 2D transforms
* Background image
* HTML5 form features
* Semantic elements
* Placeholder-shown CSS pseudo-class
* Web Authentication API
* Theme-color Meta Tag

etc then your website will fail to perform on Opera Mini browsers.

### With Firefox Browser:

Firefox usually supports the most latest technologies. Mozilla is a trend setter in web tech. However, there are still some elements that Firefox browsers do not support fully such as:

* Filesystem & FileWriter API
* Web SQL Database
* XHTML+SMIL animation
* EOT fonts

### With Safari

Shared Web Workers,CSS overflow-anchor, Web Authentication API, if used will not work at all in safari browsers. However, safari partially supports some of the features like HTML5 form features, CSS Masks. So these features if used may also lead your website to not work properly in Safari browsers.

### Use Separate Stylesheets For Different Browsers

This will save you from a heck of stylesheet problem. You can link to different stylesheet for every browser using conditional comments. So that Chrome will render chrome’s stylesheet, Firefox will go for its stylesheet and so on.

The basic conditional comment will look something like this:

```markup
<!-- [if IE ]>
    <link href="iecss.css" rel="stylesheet" type="text/css">
<![endif]-->
```

Or you can try that.

```markup
<!-- [If IE]>
    <link type="text/css" href="IEHacks.css" />
 <![endif]-->
 <!-- [if !IE]>
    <link type="text/css" href="NonIEHacks.css" />
 <![endif]-->
```

{% hint style="info" %}
[w3 validator](http://validator.w3.org/) is the only tool you need to validate HTML of your website
{% endhint %}

## Why is it generally a good idea to position CSS `<link>`s between `<head></head>` and JS `<script>`s just before `</body>`? Do you know any exceptions?

**Placing `<link>`s in the `<head>`**

Putting `<link>`s in the head is part of proper specification in building an optimized website. When a page first loads, HTML and CSS are being parsed simultaneously; HTML creates the DOM (Document Object Model) and CSS creates the CSSOM (CSS Object Model). Both are needed to create the visuals in a website, allowing for a quick "first meaningful paint" timing. This progressive rendering is a category optimization sites are measured in their performance scores. Putting stylesheets near the bottom of the document is what prohibits progressive rendering in many browsers. Some browsers block rendering to avoid having to repaint elements of the page if their styles change. The user is then stuck viewing a blank white page. Other times there can be flashes of unstyled content (FOUC), which can shows a webpage with no styling applied.

**Placing `<script>`s just before `</body>`**

`<script>`s block HTML parsing while they are being downloaded and executed. Placing the scripts at the bottom will allow the HTML to be parsed and displayed to the user first.

An exception for positioning of `<script>`s at the bottom is when your script contains `document.write()`, but these days it's not a good practice to use `document.write()`. Also, placing `<script>`s at the bottom means that the browser cannot start downloading the scripts until the entire document is parsed. This ensures your code that needs to manipulate DOM elements will not throw and error and halt the entire script. If you need to put `<script>` in the `<head>`, use the `defer` attribute, which will achieve the same effect of downloading and running the script only after the HTML is parsed.

## What is progressive rendering?

Progressive rendering is the name given to techniques used to improve the performance of a webpage (in particular, improve perceived load time) to render content for display as quickly as possible.

It used to be much more prevalent in the days before broadband internet but it is still used in modern development as mobile data connections are becoming increasingly popular (and unreliable)!

Examples of such techniques:

* Lazy loading of images - Images on the page are not loaded all at once. JavaScript will be used to load an image when the user scrolls into the part of the page that displays the image.
* Prioritizing visible content (or above-the-fold rendering) - Include only the minimum CSS/content/scripts necessary for the amount of page that would be rendered in the users browser first to display as quickly as possible, you can then use deferred scripts or listen for the `DOMContentLoaded`/`load` event to load in other resources and content.
* Async HTML fragments - Flushing parts of the HTML to the browser as the page is constructed on the back end. More details on the technique can be found [here](http://www.ebaytechblog.com/2014/12/08/async-fragments-rediscovering-progressive-html-rendering-with-marko/).

## Have you used different HTML templating languages before?

Yes, Pug (formerly Jade), ERB, Slim, Handlebars, Jinja, Liquid, just to name a few. In my opinion, they are more or less the same and provide similar functionality of escaping content and helpful filters for manipulating the data to be displayed. Most templating engines will also allow you to inject your own filters in the event you need custom processing before display.

## What will happened after you press the enter of a URL?

1. You enter a URL into a web browser
2. The browser looks up the IP address for the domain name via DNS
3. The browser sends a HTTP _request_ to the server
4. The server sends back a HTTP _response_
5. The browser begins rendering the HTML
6. The browser sends requests for additional objects embedded in HTML (images, css, JavaScript) and repeats steps 3-5.
7. Once the page is loaded, the browser sends further async requests as needed.

## Any ideas on web accessibility?

### **1. Make Sure Your Site Is Keyboard-Friendly**

The most common way of navigating using a keyboard is with the Tab key. This will jump between areas on a page that can have [‘keyboard focus,’](https://docs.microsoft.com/en-us/dotnet/framework/wpf/advanced/focus-overview) which includes links, buttons, and forms. Therefore, your goal should be to ensure that all web content and navigation can be accessed using Tab.

### **2. Make Sure All Content Is Easily Accessible**

One way you can do this is by using [ARIA landmarks](https://accessibility.oit.ncsu.edu/it-accessibility-at-nc-state/developers/accessibility-handbook/aria-landmarks/). These are tags you add to content in order to clearly define it on the page. You can tag [dynamic content](https://webaim.org/techniques/aria/#dynamic) as a ‘live region,’ which enables screen readers and similar devices to understand the content as it changes.

### **3. Add Alt Text to All Images**

As if that weren’t enough, alt text can also help you [improve your site’s SEO](https://yoast.com/image-seo-alt-tag-and-title-tag-optimization/), giving search engines more information to crawl. Just make sure to write descriptive summaries of each image, and try to include your keywords whenever it makes sense.

### **4. Choose Your Colors Carefully (For UX)**

There are plenty of online tools you can use to find and test color combinations. [WebAIM has one](https://webaim.org/resources/contrastchecker/), and we also [like Contrast Checker](https://contrastchecker.com/) because it gives you a score in real-time. The latter tool also enables you to switch to monochrome to get a rough idea of how effective any given combination is.

### **5. Use Headers to Structure Your Content Correctly**

Another key task to make your site accessible is [structuring your content](https://www.w3.org/WAI/tutorials/page-structure/headings/) by using headers carefully. Doing this will make your content much easier to understand and digest and improves flow.

Additionally, clear headers also help screen readers interpret your pages. This makes it much easier to [provide in-page navigation](https://www.nomensa.com/blog/2017/how-structure-headings-web-accessibility). It’s also simple to do as you only need to ensure you use the correct heading levels in your content.

For instance, you should [only use one H1 per page](https://codex.wordpress.org/Designing_Headings) – usually as the page title. This can be followed by subheadings starting with H2, which can then be nested further with H3, followed by H4. These should always be used in order so you should avoid using an H4 directly after an H2 (and so on).

### **6. Design Your Forms for Accessibility**

Forms are a useful addition to most sites but must be designed carefully. What’s most important is to ensure that each field is [clearly labeled](https://webaim.org/techniques/forms/). You should also aim to place the labels adjacent to the respective fields. While a sighted user can easily match a label to the corresponding field or option, this may not be obvious for someone using a screen reader.

You should also aim to [provide instructions and information](https://www.w3.org/WAI/tutorials/forms/) in a clear way that the user can easily understand. To create accessible forms in WordPress, you can use a tool like the [Caldera Forms builder](https://calderaforms.com/). This is a plugin specifically focused on accessibility, which will make your job much easier.

### **7. Don’t Use Tables for Anything Except Tabular Data**

When it comes to displaying data, tables are handy. They make it much easier for all users, including those using assistive technology, to parse a large amount of data. To get the maximum benefit, however, you’ll want to keep your tables [as simple as you can](https://make.wordpress.org/accessibility/handbook/markup/tables/).

In addition, it’s best to avoid using tables for anything but tabular data. For example, you should never use a table for layouts, lists, or anything else. This can be confusing to screen readers and similar devices.

### **8. Enable Resizable Text That Doesn’t Break Your Site**

Most devices and browsers will enable users to resize text, which can be helpful for those with visual impairments. However, if you don’t build your site to support this feature, resizing text could break your design or make it difficult to interact with your site.

A good practice is to [avoid absolute units](https://make.wordpress.org/accessibility/handbook/design/font-sizes-and-resize-text/), such as specifying text size using pixels. Instead, use relative sizes, which enable the text to scale depending on other content and screen size.

You should also never [turn off user scalability](https://make.wordpress.org/accessibility/handbook/design/font-sizes-and-resize-text/#viewport) as this will make it difficult for users to resize the text at all.

To make sure your site meets these criteria, test your font sizes thoroughly by increasing the zoom level in your own browser. If you notice that content becomes difficult to read or navigate, you can check out [this guide by WebAIM](https://webaim.org/techniques/fonts/#font_size) that discusses font size.

### **9. Avoid Automatic Media and Navigation**

Automatically-playing media files have been a bane of internet users since the [days of MySpace](https://techcrunch.com/2009/08/18/myspace-disables-auto-play-of-profile-songs-to-get-streaming-costs-under-control/). As annoying as it can be to have music or videos start when a page loads, this is an even bigger issue [in terms of accessibility](https://www.abilitynet.org.uk/news-blogs/why-autoplay-accessibility-issue).

For example, figuring out how to turn off the media can be difficult when using a screen reader, while other users could simply be confused or even frightened by the sudden noise. You should therefore avoid including elements that start without the user first prompting them.

It’s also best to avoid automatic navigation, such as [carousels and sliders](https://www.w3.org/WAI/tutorials/carousels/). This can be incredibly frustrating if the viewer needs more time to absorb all the information before moving on to the next slide or section.

## SEO in HTML

Please [follow this page](https://9elements.com/seo-cheat-sheet/).
