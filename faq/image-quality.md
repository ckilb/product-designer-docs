---
nav_order: 50
parent: FAQ
---

# How does image quality calculation work?

If your customers add an image to the canvas area they will get informed about the image quality of that image.
The quality indicator can have the following states:

- Great image quality
- Medium image quality
- Poor image quality

For calculating the image quality the following variables are used:
- The size of the original image
- The scaled size of the image placed on the canvas
- The *rendering factor* in your configuration

## Calculation 

Let's assume your product designer configuration has
- a canvas width of 1.000 px
- a canvas height of 500 px
- a *rendering factor* of 2

This basically means that the export file you will get when you generate the design in the backend has
- a width of 2 * 1.000 = 2.000 px
- a height of 2 * 500 = 1.000 px

Now let's assume the customer places an image on the canvas which has a width and height of 100 px.
For great image quality no *information* should be lost so that image's scaling size should be no more than 50 x 50 px.

If the customer places that image with a scaled size of 50 x 50 px and you generate that design in your backend with a rendering factor of 2
the size of that image inside the export file will be 100 x 100 px. No information are lost because the original image *has* the required size of 100 x 100px.

Again, if the customer places that image with an even lower scaling size, like 40 x 40 px and you generate that design the final image in your export file will be 80 x 80px.
Because the original image file is 100 x 100 px and 80 x 80px is lower than the original image file no information will be lost.

So if the rendering logic has to scale the image to a **scaling factor of 1** or less the image quality will be great. 

-----

Now let's assume the customer places that image on the canvas but this time it's scaled to 60 x 60px.
Now the final image size in the exported file will be 120 x 120 px. 
As the original image only has 100 x 100 px the rendering logic has to scale the image with a *scaling factor of 1.2* compared to the original image.
Information will be lost. 
The image quality will be *medium* because the scaling factor is higher than 1 but less then 2.

-----

The image quality will be poor if the required scaling factor is higher than 2.
That means the customer places an image with original size of 100 x 100px to the canvas and scales it to a size bigger than 100 x 100px - so the image size inside the export file will be 
bigger than 200 x 200px.


## How to change the behaviour?

If you want to have the image quality calculation more strict -> increase the *rendering factor*. \
If you want to have thge image quality calculation less strict -> decrease the *rendering factor*.

The *rendering factor* should be as high as needed but as low as possible.

You can also customize that behaviour
- either using [Monkey patching](/customizations/monkey-patching.html) 
- or adding a plugin which will replace the image quality component: [Source code plugins](/customizations/plugins.html)
