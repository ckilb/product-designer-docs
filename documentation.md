# KILB Product Designer Documentation

- [Introduction](#introduction)
- [Supported export formats](#supported-export-formats)
- [Customize Fonts](#customizing-fonts)
- [Missing features](#missing-features)
- [Extending Product Designer](#extending-product-designer)
    * [Product Designer CSS](#product-designer-css)
    * [Product Designer JavaScript](#product-designer-javascript)
    * [PHP](#php)
    * [PostMessage JavaScript](#postmessage-javascript)

### Introduction

This document will provide useful information about the KILB Product Designer
extension. It will answer frequently asked questions and gives an introduction how
to extend the plugin with programming skills.

We hope the documentation will answer *your* questions, too.

There are a few requirements you should bring with you to use and work with the plugin:
- You are familiar with the shop system (Shopware, WooCommerce) you are using.
- You read this document.
- If there's functionality missing that you require to solve your needs you probably need coding skills. See [Missing features](#missing-features)
 section.

### Supported export formats

#### WebP
WebP is a pixel-based image format implemented by Google similar to PNG. It supports
transparency. You can configure what size the image will be created by the 
canvas height, canvas width and rendering factor of your configuration.

#### SVG

SVG is a vector format. Please mind that uploaded images and clip arts
will be externally referenced. If you remove these imagem files on your 
server they cannot be loaded in the  SVG anymore.

Please also mind that some SVG viewers don't support externally references
images. 

We officially support and recommend Google Chrome as your SVG viewer.
If your SVG software doesn't show the SVG properly please try Chrome 
first before contacting support.

#### JSON
This is useful for developers. You can use the JSON to create a new
HTML canvas with Fabric.js - see http://fabricjs.com/docs/fabric.Canvas.html#loadFromJSON

### Customizing fonts

By default the product designer ships with a bunch of fonts.
If you want you can use your own list of fonts the customer can choose from.
Please mind that there's no support from our side for your own fonts. If one of your fonts
doesn't work as expected you probably cannot use it.

After you successfully set up the product designer and created a configuration for one of your articles you will
find a new directory "Product Designer - Fonts" inside the media manager in the backend of your shop system.
If you place at lease one file here your own fonts will be used. If you remove all the files in the directory again the
default fonts will be used.  
Please mind that only fonts will be used if the following requirements are met:
- it's a valid TTF font
- the extension of the file is exactly `.ttf`
- there's only numbers and letters in the file name - no other characters are allowed
- the first character of the file name must be an upper case letter (A-Z)
- file names of fonts in bold type end with `-Bold.ttf`. If there's no file for the bold type existing the customer can't set the text to bold for this font.
- file names of fonts in italic type end with `-Italic.ttf`. If there's no file for the bold type existing the customer can't set the text to italic for this font.
- file names of fonts in bold & italic type end with `-BoldItalic.ttf`. If there's no file for the bold & italic type existing the customer can't set the text to both bold & italic for this font.
  
Some examples for valid file names are:
- Audiowide.ttf
- OpenSans.ttf
- OpenSans-Bold.ttf
- OpenSans-Italic.ttf
- OpenSans-BoldItalic.ttf

### Missing features

The product designer is by nature a big plugin with a lot of functionality that
hopefully cover your use cases as well. Still we found out that a lot of customers
of the plugin have very specific requirements.

The plugin will be extended and improved in frequent intervals.
If there's some functionality that is missing from your point of view you can
- contact our support and *ask* if the functionality is maybe planned within one of the next releases. We're always open to new ideas. Please mind that
  there's no guarantee a feature you need will be implemented. That's why we offer you the possibility to test our product for several weeks for free.
- extend the product designer by yourself. This requires coding skills. See [Extending Product Designer](#extending-product-designer) section.

### Extending product designer

There are several ways to extend the product designer. 
For this you need knowledge in programming, especially PHP, JavaScript and fabric.JS. 
Please mind that we can't offer you support for issues that were created by
your own modifications. If something isn't working as expected please remove ALL customizations you did
and try again before contacting support.


#### PHP

For the backend part of the product designer you can use extension functionality
of the E-commerce-system you are using.
There are great developer documentations existing:
- Shopware 6: https://docs.shopware.com/en/shopware-platform-dev-en
- WooCommerce: https://docs.woocommerce.com/document/woocommerce-developer-wiki/

#### Product Designer JavaScript

You can embed your own JavaScript code to the Product Designer frontend.
In the backend of the product designer, edit a configuration and click on the
"Advanced" tab. Enter the URL of your JavaScript file here and don't 
forget to save the configuration afterwards.

From now on the JavaScript file will be loaded right after the
core JavaScript of the designer has been loaded.

The first thing you should do inside of your JavaScript code is to subscribe
to the `onCanvasInitialized` event. This event will be thrown 
by the product designer every time a canvas was initialized.
If you only have one configuration assigned to your article this event
will be fired just once.
If you have multiple configurations assigned
(e.g. "T-Shirt, front side", "T-Shirt, back side") the event will be  fired 
for every canvas of each configuration.

The `configuration` and the `canvas` will be passed to the event listener.  
`configuration` is basically a simply key-value object containing all the 
configuration information set in the backend.  
`canvas` is  an object of type [fabric.Canvas](http://fabricjs.com/docs/fabric.Canvas.html). See the
Fabric.js documentation for further information.

```javascript
window.productDesigner.onCanvasInitialized = (configuration, canvas) => {
    console.log('Configuration: ', configuration);
    console.log('Canvas:', canvas);
}
```

With access to the fabric Canvas you have a lot of options
to modify the behavior of the functionality. For better understanding
here is a small code snippet that will:
- remove the ability to drag & drop text elements on the canvas
- uppercase all the letters of the text element

```javascript
window.productDesigner.onCanvasInitialized = function (configuration, canvas) {
  canvas.on('object:added', (event) => { // will be fired if a new element was placed on the canvas
    const obj = event.target; // get the element placed on the canvas

    if (!obj.hasOwnProperty('text')) {
      return; // don't consider non-text elements
    }

    // lock movement
    obj.lockMovementX = true;
    obj.lockMovementY = true;

    // set all characters to upper case
    obj.text = obj.text.toUpperCase();
  });

  canvas.on('text:changed', (event) => {
    const obj = event.target; // get the element placed on the canvas

    // set all characters to upper case
    obj.text = obj.text.toUpperCase();
  });
}
```

In some cases you might want to know what configuration is currently active.
By default this is  always the first configuration assigned to the article.

See the following snippet to find out how to get the current active configuration:
```javascript
// use event that will be fired when active configuration has been changed by customer
window.productDesigner.onConfigurationSwitched = (configuration) => {
    console.log('Current configuration is: ', configuration);
};

// additionally you can use getCurrentConfiguration() in your code to find out the active configuration
window.setTimeout(() => {
    console.log('Current configuration is: ', window.productDesigner.getCurrentConfiguration());
}, 5000);
```

Please mind that of course you are also able to modify the DOM, i.e., to add your own elements.
```javascript
const informationTextElement = document.createElement('div');

informationTextElement.innerText = 'Dear customer. Thanks for using the product designer.';

// this add some styles to the div element for demonstration purposes. it's better to set these via custom CSS.
informationTextElement.style.position = 'absolute';
informationTextElement.style.top = '50%';
informationTextElement.style.left = '50%';
informationTextElement.style.transform = 'translate(-50%, -50%)';
informationTextElement.style.backgroundColor = 'white';
informationTextElement.style.color = 'red';
informationTextElement.style.cursor = 'pointer';
informationTextElement.style.padding = '50px';
informationTextElement.style.zIndex = '999999';

informationTextElement.onclick = () => {
  informationTextElement.remove();
}

document.body.append(informationTextElement);
```


#### Product Designer CSS

You can add your own stylesheet to the product designer to modify the
appearance of it. 

In the backend of the product designer, edit a configuration and click on the
"Advanced" tab. Enter the URL of your CSS file here and don't
forget to save the configuration afterwards.

From now on the CSS file will be loaded right after the
core JavaScript of the designer has been loaded.

Here are some example styles:
```css
.open-modal-qr-code { /* hide QR code button */
  display: none !important;
}

.open-modal-image-upload { /* hide image upload button */
  display: none !important;
}

#options-component-style .color { /* hide button to change text color */
  display: none !important;
}
```

#### PostMessage JavaScript

By embedding your own [JavaScript](#product-designer-javascript) you are able to
change the functionality of the product designer itself.

Additionally you are able to modify the behaviour and functionality of what happens
when the user applied a design inside your E-Commerce shop system.

The product designer is loaded in an iframe. When the user applies the design 
some data like the basket image preview image URL will be passed from the iframe to the shop system
via JavaScript's native postMessage API. 

You can use this API for your own purposes.

For this you need to extend the JavaScript of your shop theme. 
You can find out how to do this inside the documentation of the shop system you are using:

- Shopware 6: https://docs.shopware.com/en/shopware-platform-dev-en
- WooCommerce: https://docs.woocommerce.com/document/woocommerce-developer-wiki/

Here is an example how to subscribe to the PostMessage event & load the preview image in your own
img element. You could use this to replace the original product image.

```html
<img id="preview-image" />
<script type="text/javascript">
    window.addEventListener('message', (event) => {
        let data;

        try {
            data = JSON.parse(event.data);
        } catch (e) {
            return;
        }

        if (true !== data.productDesigner) {
            return;
        }

        if ('setDesign' !== data.action) {
            return;
        }

        console.log(data.params.canvasData); // array of canvas-configuration mappings

        document.getElementById('preview-image').src = data.params.basketImageUrl;
    });
</script>
```
