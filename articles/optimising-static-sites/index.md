# Optimising a Static Site: Best Practises

## Table of Contents

## Introduction

Static sites by default are lean and fast compared to full-stack web applications since there's no server-side code involved (except if you use [serverless functions](https://docs.netlify.com/functions/build-with-javascript)). However, there are best practises to get the page load speed possible. 

For example, it would defeat the purpose of choosing a static site if you had a 10MB image displayed.

In this article, you'll learn the best practises for optimising a static site such as image optimisation, CSS and JS minification and the best location to include stylesheets and scripts. 

Also, you'll learn the ideal use cases for different optimisation methods such as using a content delivery network (CDN) for assets versus hosting them locally, bundling scripts and stylesheets together versus seperately and if it's ever a good idea to write inline CSS and JS.

Finally, you'll discover different speed-testing tools, find out which matters most and the metrics you should pay attention to.

## Three Ways to Optimise Your Static Site


### A Brief Guide to Image Optimisation

Having gorgeous full-width images and photo galleries can make your website stand out but they can also slow down your site. There's no reason to have a 2560x1080px image if your website only displays it at 800x400px. 

A sensible default is to resize your images to be 1920x wide as a maximum but the best approach is to inspect your images by right clicking on them and selecting view image info which will tell you the image's dimensions. Do this for every image using a browser window that's the highest resolution you expect your visitors to have and then resize them to that size.

Sites like [TinyPNG](https://tinypng.com) and [ShortPixel](https://shortpixel.com/online-image-compression) can optimise PNG and JPG files further using lossy (or in ShortPixel's case, lossy, glossy or lossless) compression to reduce file sizes further but this can also be handled manually using Photoshop's Save for Web export option where you can specify size, file format and quality. 

As a general rule, all non-transparent images should be converted to JPGs with the quality set to 70 which should provide a good balance between size and quality.  

However, there is a even more efficient file format that can be used, webP. As with other image formats, there are plenty of online conversion sites that support webP ([WebP Converter](https://webp-converter.com) is but one of them) that will convert image files to and from webP. For more control, [WebPShop](https://github.com/webmproject/WebPShop) is a Photoshop plugin that will allow you to open and save WebP files and it also provides quality settings. *Note:* You must export your image via Save or Save As for the plugin to work.

[/engineering-education/optimising-static-sites.png](Can I Use WebP image format table)

Unfortunately, while WebP support is widespread across browsers and operating systems, it isn't universal. According to [Can I Use](https://caniuse.com/?search=webp), Safari support is limited to the latest OS versions (macOS Big Sur and iOS/iPadOS 14 and above) and Internet Explorer doesn't support it all so a fallback would need to be provided. That's where the `<picture>` and `<sourceset>` elements come in. They can be combined to serve multiple image formats for a single image similar to the `<audio>` and `<video>` elements. 

**Note:** The other browsers can be served with [more efficient formats](https://www.joshwcomeau.com/performance/embracing-modern-image-formats) (JPEG 2000 and JPEG XR for older versions of Safari and Internet Explorer respectively) but with the effort it takes to convert every image to two additional formats, a well-optimised JPG and PNG would suffice.

```html
<picture>
  <source srcset="img/niceNewImageFormat.webp" type="image/webp">
  <source srcset="img/normalImageNewElement.jpg" type="image/jpeg"> 
  <img src="img/sameNormalImage.jpg" alt="Normal Alt Text">
</picture>
```
See [CSSTricks](https://css-tricks.com/using-webp-images) for a more detailed guide to using WebP images including in CSS (for background images, for example.)

**Briefly cover image optimisation and link to Section article with further detail - one you reviewed**

### Best Practises to Stream Videos

Not just stream videos and display auto-play. It's much more performant to load the video thumbnail as an image and then only display the video iframe when a user chooses to play the video (and thus load YouTube's JS).

Link to CSSTricks article

## Libraries Icons and JS/CSS etc.

Instead of hosting the whole thing (minified, slim or not). Just include the pieces you need. Code coverage tools can help with this.

### CSS and JS Minification

Cover CSS and JS Minification. Mention tools that do this manually and automatically. Mention libraries often come in a slim and minified format and explain this.

Can have unminified files in root folder and manually minified ones in a public folder. Netlify let's you easily pick publication folder in Git Repo.

## When Opposing Optimisation Methods Collide - The Ideal Use Cases of Each?


### Should you use CDNs for JS libraries and fonts or host them locally?

Mention the fastest Google Font code (preload etc.) from CSS Wizardry site and the difference between FOUT and flashes of unstyled text etc.

Mention variable fonts and picking only needed weights.

Users may already have CDNs cached.

### Is it better that bundle scripts and stylesheets together or use them seperately? 

Reducing requests to bundle them together. Better if code in scripts and stylesheets is used in every page. Mention bundling tools.

If code is only used on certain pages, better to split the CSS file into multiple and link to them on only required pages. Use my site as an example (animation.css/testimonial.js)

### Is it ever okay to write inline CSS and JS

For unique styles and scripts, only needed in one place, it's best to inline it for best performance.

You can also use an optimisation method called critically inline which means all the necessary code for the webpage to function is inlined and the extra code is contained in stylesheets and scripts and its loading is deferred. Tools like [Pegasus](https://pegasaas.com/critical-path-css-generator/) will automatically generate the critical CSS for your site.

## Speed Testing Tools

use Eleventy leaderboard/Speedlify/Google Lighthouse as speed testers

## The Most Important Speed Testing Tools

Discover different speed-testing tools, find out which matters most and 

## The Most Important Metrics in Speed Tests

the metrics you should pay attention to.

## Conclusion

Link to similar Section WordPress article you reviewed (and perhaps in Introduction too). 

Mention Eleventy as an alternative to Node.js and WordPress and link to relevant articles (Eleventy and Node.js)