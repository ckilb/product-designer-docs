---
parent: Customizations
nav_order: 4
---

# Post Message API

The moment the customer finishes the design the product designer will be closed. Additionally a post message will be sent
from the designer's iframe to the HTML page of your web shop.

This is done to pass some required information - like the preview image of the design and the price - to your web shop, so it can
be displayed there.

If you like you can listen for this post message and handle it on your own.
The listener has to be implemented inside the JavaScript of your online shop system. So please read the developer documentation
of your shop software to find out how to extend it.

To find out the content of the payload of the post message please check out the [source code](/customizations/source-code.html) and 
have a look into the `PostMessagePayload` type definition.

## Example 

The following JavaScript will listen for the post message, get the preview image URL form inside it and injects it into the
image gallery of the product.
Please mind that this is just an example. It's based on the default template of Shopware 6 and there's not guarantee this will work
out of the box. It should just give you an idea how it works:

```javascript
window.addEventListener('message', (event) => {
    let data;

    try {
        data = JSON.parse(event.data);
    } catch (e) {
        return; // if JSON-decoding is not possible, the post message does not contain valid JSON - so it can't be a post message from the product designer
    }

    if (true !== data.isProductDesigner) { // if the post message contains valid JSON this doesn't mean it has to come from product designer, so check for this flag is necessary
        return;
    }

    const imageUrl = data.params.basketImageUrl; // get the basket image preview URL
    const sliderImage = document.querySelector('.product-detail-media .tns-slide-active img[itemprop=image]'); // get the product image inside slider
    const singleImage = document.querySelector('.product-detail-media .gallery-slider-single-image img[itemprop=image]'); // get the single product image in case no slider exists

    [sliderImage, singleImage].forEach(img => { // replace the source URL of the images found
        if (!img) {
            return;
        }

        img.removeAttribute('srcset');
        img.src = imageUrl;
    })
});
```



