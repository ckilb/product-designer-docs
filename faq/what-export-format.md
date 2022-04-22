---
nav_order: 2
parent: FAQ
---

# What export file format should I use?

You can export the designs of your customers in SVG or a pixel-based format like WEBP or JPG. Both is supported.

Our recommendation is to use **WEBP** because of it's small file size and support of transparency.
If the software you use for printing the design is not supporting **WEBP** files then **JPG** is a good choice in case you
don't need transparency. If you need transparency support **PNG** should be fine.
By configuring the rendering factor in your product designer configurations you can specify the size/quality of the exported images.

In general we don't recommend **SVG** file export. For sure vector-based images like SVGs have it's advantages like
a very small file size and scaling without losing quality.
The drawback of SVG files is that they can look different depending on the software you use.
Usually SVGs created by the designer work perfectly in your browser like Chrome or Firefox. And there is a good chance
it will work in Inkscape, too. Most likely it will not work in Illustrator because it doesn't support some features
like inline embedding of images.

That's because every SVG viewer software has it's own implementation of how to parse and interpret SVG files and they don't work exactly the same.
Also they often don't support all the functionalities SVG in theory could have.

So if you decide to use SVG please be sure to test your work flow - starting with creating a design using the product designer and finishing with 
have a look to the customized product you would sell to your customers.

Please mind that - if you allow your customers to upload their own image files to use them in their design - these image
files most likely are not vector-based. So the advantage of SVGs to be scalable without quality loss is lost anyway.

