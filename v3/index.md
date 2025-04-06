---
title: Version 3
nav_order: 3
has_children: false
---

# Version 3

The third major version of KILB Product Designer is a huge update introducing countless improvements - making the designer probably one of the most sophisticated and polished product customization software on the market.
The update will not only contain a good amount of improvements you'll immediately see, but also a lot of updates under the hood - using the newest technology. 

## What's new?

### Theme Colors
- Specify the primary and secondary color to be used in the designer. Like with all settings you'll be ablte to specify such colors for each configuration and article individually.
- The default color will be a neutral black one, which will probably fit nicely to your shop's theme. You want that greenish color back? Just set the primary color of your configuration to "teal".

### Improved Performance
- The performance of the designer has been drastically improved. Once your customers click the button to open it, it will be loaded almost immediately.
- We also replaced the old "Bootstrap" modal with our own. The new one is not only faster, it also gives more space for the design because no header bar is needed anymore.

### Improved UI & Design
You might have compared our product designer with others. You might have recognized that our designer's user interface and design is much cleaner and sophisticated. Still, there was room for improvement. So we improved it: \
Almost all design elements (buttons, dropdowns etc.) are now based on PrimeVue - a state of the art component library for designing browser software. PrimeVue is used by thousands of websites - because they know what they do. Our product designer won't reinvent the wheel anymore implementing its own elements. \
Now you can be sure, that almost every element is thoroughly tested by experienced UI/UX designers and will work greatly on a lot of devices.\
Also, we rearranged some elements - primarily to save space for the design: Your customers need to see the design as large as possible - so they can easily work with it, even on mobile devices. Therefore, all other elements should be large enough to nicely interact with them, but don't take too much space.

### Refactoring of Surcharges
As you probably know, you can specify prices according to the content of your customer's designs.\
In previous versions, these additional prices had simply been added to the original price of the article.
This has some downsides regarding book keeping, tax calculations etc. - so we've changed it.\
In Version 3, the item will be added into cart with its original price. Additionally, another surcharge cart item will be added. Your customer's won't be able to remove one of the items without the other.

### Auto-Rendering
In the Backend you'll now find a new tab "Auto rendering". If you keep it open, all designs, including newly ordered ones, will be automatically rendered - saving you some time. \
There's still our extension plugin "KILB Rendering Service" which will also automatically generate designs on our servers. This is the most convenient solution, but it requires an additional license - and we'll try to get most of its convenience into the designer mid-term - without any additional costs.\
Implementing Auto-Rendering is the first step.

### Disable Article Image in Preview Image
Once your customers finished their design, our designer will automatically create a preview image - which is basically the article image with the individual design placed on top of it.\
This is a great feature, because your customers will show your customers how the final product will look like.\
We found out that some of you use the article image in a different way and it in such cases it doesn't make sense to add the image behind the design. Therefore, this is now a configuration option you can enable or disable.


### Technical Improvements
We said, we did a lot of improvements under the hood. \
If you don't mind the technical details, stop reading now. If you're a developer or interested in programming and/or tech, you'll might find this interesting:

- Most direct usages of promises were replaced with await/async for better readability.
- Neverthrow library was completely removed, because it didn't work well with async/await in some cases.
- Fabric.JS has been updated from version 5 to 6 - the biggest benefit is ES6 support, which will make the final build smaller thanks to tree-shaking and improves maintanability and readability of the code.
- All packages have been updated to their newest version - including Vue.js.
- Our product designer contains many parts (Backend, Frontend, Plugin for Shopware, Plugin for Wordpress etc.) - most of its repositories have been merged into a single Mono repo. This will greatly improve efficience in developing. Unfortunately, the Monorepo is not yet open-sourced. We are working on it. If you need access to the source code right now, don't hesitate to reach out.
- E2E testing using Playwright has been added.
- Linting using ESLint, Prettier and PHP CSFixer has been approved.
- Simplified build pipeline using Github Actions.