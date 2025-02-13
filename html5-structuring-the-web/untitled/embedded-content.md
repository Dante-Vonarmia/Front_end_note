# Embedded content

## How to keep page loading efficiency while using iframe?

In order to improve speed, it's a good idea to set the iframe's `src` attribute with JavaScript after the main content is done with loading. This makes your page usable sooner and decreases your official page load time (an important [SEO](https://developer.mozilla.org/en-US/docs/Glossary/SEO) metric.)

## What common security concerns in embedded technique?

### ClickJacking

[Clickjacking](https://en.wikipedia.org/wiki/Clickjacking) is one kind of common iframe attack where hackers embed an invisible iframe into your document (or embed your document into their own malicious website) and use it to capture users' interactions. This is a common way to mislead users or steal sensitive data.

### **Only embed when necessary**

Sometimes it makes sense to embed third-party content — like youtube videos and maps — but you can save yourself a lot of headaches if you only embed third-party content when completely necessary. A good rule of thumb for web security is _"You can never be too cautious. If you made it, double-check it anyway. If someone else made it, assume it's dangerous until proven otherwise."_

### **Use HTTPS**

[HTTPS](https://developer.mozilla.org/en-US/docs/Glossary/HTTPS) is the encrypted version of [HTTP](https://developer.mozilla.org/en-US/docs/Glossary/HTTP). You should serve your websites using HTTPS whenever possible:

1. HTTPS reduces the chance that remote content has been tampered with in transit,
2. HTTPS prevents embedded content from accessing content in your parent document, and vice versa.

> However, because of the second benefit of HTTPS above, _no matter what the cost, you must never embed third-party content with HTTP._ (In the best case scenario, your user's Web browser will give them a scary warning.)&#x20;

## About Flash?

{% hint style="info" %}
Just leave it rest in peace, will ya? 👌🏻
{% endhint %}

* **Broaden your reach to everyone.** Everyone has a browser, but plugins are increasingly rare, especially among mobile users. Since the Web is easily used without any plugins, people would rather just go to your competitors' websites than install a plugin.
* **Give yourself a break from the** [**extra accessibility headaches** ](https://webaim.org/techniques/flash/)**that come with Flash and other plugins.**
* **Stay clear of additional security hazards.** Adobe Flash is [notoriously insecure,](https://www.cvedetails.com/product/6761/Adobe-Flash-Player.html?vendor_id=53) even after countless patches. In 2015, Alex Stamos, then-Chief Security Officer at Facebook,  [requested that Adobe discontinue Flash.](https://www.theverge.com/2015/7/13/8948459/adobe-flash-insecure-says-facebook-cso)

{% hint style="warning" %}
Due to its inherent issues and the lack of support for Flash, Adobe announced that they would stop supporting it at the end of 2020.  As of January 2020, most browsers block Flash content by default, and by December 31st of 2020, all browsers will have completely removed all Flash functionality. Any existing Flash content will be inaccessible after that date.
{% endhint %}

Instead of relying on Adobe Flash, you should use [HTML5 video](https://developer.mozilla.org/en-US/docs/Learn/HTML/Howto/Add_audio_or_video_content_to_a_webpage) for your media needs, [SVG](https://developer.mozilla.org/en-US/docs/Learn/HTML/Howto/Add_vector_image_to_a_webpage) for vector graphics, and [Canvas](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial) for complex images and animations.&#x20;
