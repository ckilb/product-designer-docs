---
nav_order: 200
parent: FAQ
---

# How can I decrease the initial zoom?

If you set up the product designer configuration correctly - so your article image has no blank space around, the width and height of the article image and the canvas are correctly defined - you most
likely don't need to change the zoom. The product designer will make sure the image and canvas will fit perfectly into the window.

If you still like to decrease the initial zoom you could simply use *monkey patching* to change the zoom once the canvas is loaded.

First create a javascript file:

`custom.js`

```javascript
const store = window.productDesigner.store;

window.productDesigner.watch(store.hasActiveCanvas(), (isActiveCanvasExisting) => {
    if (!isActiveCanvasExisting) {
        return;
    }
    
    store.setCanvasZoom(0.8); // 1 == default zoom, 0.7 == lowest possible value, 2 == highest possible value
});
```

Now upload that JavaScript file to your shop server in a directory which is publicly available.
For Shopware this is usually the directory `shopware-installation-path/public/` so the file path would be:

`shopware-installation-path/public/custom.js`

Now get the URL to the CSS file, for instance
`https://your-shop.de/custom.js` and add this JavaScript file to your product designer configuration (*Advanced* Tab).

Read more about what you can do with this kind of customizations here:
[Monkey Patching](/customizations/monkey-patching.html)
