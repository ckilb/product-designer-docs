---
nav_order: 2
parent: FAQ
---

# What export file format should I use?

You can export the designs of your customers in PDF, SVG or a pixel-based format like WEBP or JPG.

Our top recommendation is to use **WEBP** because of it's small file size and support of transparency.
If the software you use for printing the design is not supporting **WEBP** files then **JPG** is a good choice in case you
don't need transparency. If you need transparency support **PNG** should be fine.
By configuring the rendering factor in your product designer configurations you can specify the size/quality of the exported images.

In general we don't recommend **SVG** file export. For sure vector-based images like SVGs have it's advantages like
a very small file size, scaling without losing quality and the possibility to modify it.
The drawback of SVG files is that they can look different depending on the software you use.
Usually SVGs created by the designer work perfectly in your browser like Chrome or Firefox. And there is a good chance
it will work in Inkscape, too. Most likely it will not work in Illustrator because it doesn't support some features
like inline embedding of images.

That's because every SVG viewer software has its own implementation of how to parse and interpret SVG files and they don't work exactly the same.
Also they often don't support all the functionalities SVG in theory could have.

So if you decide to use SVG please be sure to test your work flow - starting with creating a design using the product designer and finishing by 
having a look at the customized product you would sell to your customers.

Please mind that - if you allow your customers to upload their own image files to use them in their design - these image
files most likely are not vector-based. So the advantage of SVGs to be scalable without quality loss is partly lost anyway.

When using pixel-based image formats like **WEBP** you can be quite sure that the image will - aside from colors - look identical on every device.
So if this a way to go for you should do so.

If you really need to have a vector-based file format you should give **PDF** a try. PDF is a very popular format in the printing industry because
it has a lot of features SVG or simple pixel-based files won't have (embedded fonts, bleed boxes, color profiles...).
PDF should be your first option if you follow the workflows of the professional printing industry. 
Please mind that PDFs have a lot of features and the PDF created by the designer may not fulfill all your requirements as not all features you need are used.
In this case please contact our support. We always have an open ear to improve our product - including the PDF export. But please also be aware
that you may have to do some post processing with your own tools based on the PDF from the designer.

## Summary

- Use **WEBP** (or **PNG** / **JPG**) if you just want to have the design printed
- Use **PDF** if you care about file size, vectors, post processing (for instance color accuracy) 
- Use **SVG** if you really know what you do. If you need vectors, favor PDF. 
