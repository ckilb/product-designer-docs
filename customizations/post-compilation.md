---
parent: Customizations
nav_order: 1
---

# Post Compilation

## Quick Start

You can customize the product designer with post compilation customizations.
With this approach you keep the asset files (JavaScript and CSS) bundled with the designer plugin
for you online shop untouched but add your own JavaScript and CSS files which will be loaded
additionally.

The following steps will explain to you how to add post compilation customizations. Please make sure that
you have installed and configured the designer beforehand.

### CSS customizations

1. Open the designer in our online shop for one of your articles.
2. Use the web developer tools of your browser and find the elements you want to change.
For most elements you should use their (or their parents) attribute `data-component` as an identifier in your CSS selectors.
3. Create a CSS file with your customizations.
4. Upload the CSS file to your server choosing a path which is publicly available.
5. Find out the URL to your CSS file, make sure it's working and copy it.
6. Open your web shops admin area, open your product designer configuration you want to apply the CSS style to, and paste the
URL into the field _Custom Stylesheet URL_ under _Advanced_.

#### Examples

Set the background color of all buttons on the left to yellow:

```css
[data-component="action"] button {
    background-color: yellow;
}
```

Remove QR code button:

```css
[data-component="action.qr-code-button"] {
    display: none;
}
```

### JavaScript Customizations

1. Open the designer in our online shop for one of your articles
2. _(optional)_ Download the Frontend source code of the product designer to get a good understand of how it works - especially the _store_ (file: _src/business/store/store.ts_).
3. Create a JavaScript file with your customizations.
4. Upload the JavaScript file to your server choosing a path which is publicly available.
5. Find out the URL to your JavaScript file, make sure it's working and copy it.
6. Open your web shops admin area, open your product designer configuration you want to apply the JavaScript functionality to, and paste the
   URL into the field _Custom JavaScript URL_ under _Advanced_.

#### How To

Because your custom JavaScript file will be simply injected into the HTML source code of the product designer
Frontend you can basically do whatever you want.

If you like to add a new element to the designer you could create a DOM element and inject it.

We also provide you the _store_ of the Vue.js application and the _watch_ method of Vue.js using the _window_ object:
- _window.productDesigner.store_ will be an instance of _Store_ inside _src/business/store/store.ts_
- _window.productDesigner.watch_ will be the [_watch_ function from Vue.js](https://vuejs.org/api/reactivity-core.html#watch)

You can use this to listen to changes to designer state variables like the active canvas or active configuration.
You are also able to access the fabric.JS canvas.

#### Pitfalls

**Please mind**: Some method of the _Store_ will return a Vue.js Ref object you can use as an argument
for the _watch_ function. If you like to get the value of an Ref object without using _watch_ make sure you
get the _value_ property:

Wrong:
```javascript
const configuration = window.productDesigner.store.activeConfiguration();

alert(configuration.name)  // fail: configuration is no instance of Configuration but Ref<Configuration> 
```

Right:
```javascript
const configuration = window.productDesigner.store.activeConfiguration().value;

alert(configuration.name); 
```
____

Always check for store.hasActiveCanvas() before reading _store.activeCanvas()_.
If you call _store.activeCanvas()_ and no active canvas is existing a JavaScript error will be thrown:

Wrong:
```javascript
const canvas = window.productDesigner.store.activeCanvas().value;
```

Right:
```javascript
if (window.productDesigner.store.hasActiveCanvas().value) {
    const canvas = window.productDesigner.store.activeCanvas().value;
}
```

____

If you make changes to the content of the canvas don't forget to render it again.

```javascript
if (window.productDesigner.store.hasActiveCanvas().value) {
   const canvas = window.productDesigner.store.activeCanvas().value;
   
   canvas.backgroundColor = 'green';
   canvas.renderAll(); // new background color will not be visible before this call
}
```

#### Examples

Inject another DIV element:

```javascript
const myDiv = document.createElement('div');

myDiv.style.width = '100px';
myDiv.style.height = '100px';
myDiv.style.backgroundColor = 'red';
myDiv.style.color = 'yellow';
myDiv.innerText = 'Thanks for using product designer!';

document.body.append(myDiv);
```

Disallow drag & dropping of images added to the canvas:
````javascript
const store = window.productDesigner.store;

window.productDesigner.watch(store.hasActiveCanvas(), (isActiveCanvasExisting) => {
   if (isActiveCanvasExisting) {
      const canvas = store.activeCanvas().value;

      canvas.on('object:added', (event) => {
         const obj = event.target;

         if (obj.type === 'image') {
            obj.lockMovementX = true;
            obj.lockMovementY = true;
            canvas.renderAll();
         }
      });
   }
});
````
