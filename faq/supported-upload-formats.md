---
nav_order: 3
parent: FAQ
---

# What upload formats are supported?

Your customers can add images to the canvas - either by uploading them or by choosing one of
the *predefined images* you uploaded before.

We can't give you a full list of supported image types here because this dependent on the browser your customers use.
The product designer uses the framework [fabric.JS](http://fabricjs.com) which is based on the 
[HTML Canvas technology](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API) implemented by the browser.

Most likely at least the following image types will work:
- JPG
- PNG
- WEBP
- GIF (first frame will be used)
- SVG (please mind: a SVG file contains a description how to draw an image - not the actual pixels themselves - which could be interpreted differently by different software)
