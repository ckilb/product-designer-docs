---
nav_order: 1
parent: FAQ
---

# What exports formats are supported?

## WebP
WebP is a pixel-based image format implemented by Google similar to PNG. It supports transparency.

## JPG
JPG is a popular pixel-based image format supported by most image viewers. The file size is small. Transparency is not supported.   

## PNG
PNG is another popular pixel-based image format supported by most image viewers. The file size is bigger compared to JPG and WEBP but it's lossless. Transparency is supported.

## SVG
SVG is a popular vector format. Please mind that uploaded images and clip arts will be externally referenced. If you remove these image files on your server they cannot be loaded in the SVG anymore.
Please also mind that some SVG viewers don't support externally references images.

If you think about using SVG or are not sure what export format is the right for you please read this:
[What export format should I sue?](/faq/what-export-format.html).

## JSON
This is useful for developers. You can use the JSON to create a new HTML canvas with Fabric.js - see 
[http://fabricjs.com/docs/fabric.Canvas.html#loadFromJSON](http://fabricjs.com/docs/fabric.Canvas.html#loadFromJSON)
