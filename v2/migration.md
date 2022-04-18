---
parent: Version 2
---

# Migration from Version 1

If you just use the designer without any customizations for JavaScript or CSS
you most likely can update the designer without any manual todos.
__Still, because the Product Designer is a highly configurable plugin you should save some time for the next update to test if everything is working as expected.__

If you added custom JavaScript or CSS you have to adjust that - version 2 will break backwards compatibility here.
The basic idea of these customization technology is still
the same - so migrating shouldn't be too hard - still some things have changed.

## CSS selectors

In version 1 a lot of elements had CSS selectors which you could use to overwrite the style.
In version 2 [TailwindCSS](https://tailwindcss.com/) is used to style the elements. Therefore CSS
class names have no semantic meaning and can't be used to identify HTML elements anymore.

Instead all the HTML templates in the designer are split in small Vue.js components and every component's
root HTML tag has - by convention - an attribute `data-component`.
So if you like to overwrite some CSS style you can use this attribute.

As an example: To add a red background color to the QR code button the code had to be like this:
````css
.open-modal-qr-code { background-color: red; }
````

For version 2 your CSS code has to similar to this:
````css
[data-component="action.action-button"] {
  background-color:red;
}
````

The new way is much more consistent and - if you use these to style your elements - compatibility for future
updates of the Product Designer is improved.

## JS store

In version 1 you were able to retrieve the `canvas` and `configuration` object via
`window.productDesigner.onCanvasInitialized`.
Additionally you were able to find out if the user switched the configuration via `window.productDesigner.onConfigurationSwitched`.

While this implementation was sufficient for most of our clients needs there are two disadvantages:
* It's not possible to retrieve other objects like canvas zoom, fonts or (background) images.
* Providing this functionality was additional code in the designer source code to take care about: When the source code of the designer was changed there was additional overhead in testing the customization functionality.

That's why in version 2 both methods, `onCanvasInitialized` and `onConfigurationSwitched` were removed.
Instead, you are now able to access the same store object that is used by the designer for all the data that have to be shared between different Vue.js components.

As an example: In version 1 you were able add an fabric.JS event similar to this:

````javascript
window.productDesigner.onCanvasInitialized = function (configuration, canvas) {
  canvas.on('object:added', (event) => {
    if (configuration.name = 'name to filter for') {
        // do something
    }
  })
};
````

In version it will work like this:

````javascript
const store = window.productDesigner.store;

window.productDesigner.watch(store.hasActiveCanvas(), (isActiveCanvasExisting) => {
    if (!isActiveCanvasExisting) {
      const canvas = store.activeCanvas().value;

      canvas.on('object:added', (event) => {
        if (configuration.name = 'name to filter for') {
          // do something
        }
      });
    }
});
````

Please mind: A lot of the objects inside `window.productDesigner.store` are `refs`. So you have to
use it's property `value` to get the actual value. Read more about this here:
[https://vuejs.org/guide/essentials/reactivity-fundamentals.html#reactive-variables-with-ref](https://vuejs.org/guide/essentials/reactivity-fundamentals.html#reactive-variables-with-ref)


`window.productDesigner.watch` is just a wrapper function around Vue.js watch. You can use it for all `ref` objects to listen
for changes. More about this here: https://vuejs.org/api/reactivity-core.html#watch

For more information feel free to have a look into the [documentation of customizations](/customizations.html).
