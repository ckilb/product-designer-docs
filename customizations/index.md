---
title: Customizations
nav_order: 2
has_children: true
---

# Customizations

There are several ways to customize the designer to your needs.
It's crucial to understand all of them to find out the way that works best for you and your team.

Please mind: For all ways of customization developer skills are needed.

Please also keep in mind that - if you've implemented a customization and it works
for you - there's still tiny risk that it will stop working after you've updated the product designer or your E-Commerce software to
a new version. So customizations of the designer are - same like running any software - most likely not a one-time charge.

If you are eligible for using our [official support](/support.html) and you have some issues using the designer please make sure
to disable all your customizations before contacting us - so you can be sure that the issues are not created by one of your customizations.

## Post compilation customizations

This is the recommended way if you or your colleagues have basic knowledge in programming and you don't want to spend too much time and money
in developing customizations and _keeping them up to date_.
The designer source code will not be touched. Instead you can still use the compiled files which are bundled into the shop plugin.
Post compilation customizations take place in _additional_ JavaScript and CSS files which will be loaded _after_ the compiled files of
the designer. Using this way you don't _replace_ logic but _extend_ it afterwards.
Therefore it's _not_ required to download the source code using this approach - still it's recommended to have a look into it to get a better understanding of what's
happening behind the scene.

While it's possible to achieve some great results there are some disadvantages using this approach though:
- It's required to load more files from the server (the JavaScript/CSS files containing the customizations).
- If your customizations are complex or need a lot of lines of code it could be hard to maintain these - because the core designer logic you modify with your customizations
  is minified and therefore hard to read. Developers won't get the whole picture.
- There's a small time frame between the loading of the core designer files and your customization files. The designer initially loads in it's original state and
  later on your customizations will be applied. This could be visible to the end user. There are smart ways to work-around that issue - like setting elements initially to hidden via CSS - but you
  have to take care about this.
- While it's quite possible to do deep customizations using this approach it can be tricky sometimes. If you need deeper ways of customization or prefer a cleaner way this approach
  may not be the right for you.

>> Read more about post compilation customizations [here](/customizations/post-compilation.html).

## Source code plugin customizations

This is the recommended way if you want to deeply change the core logic of the designer using a clean approach
and without risking too many compatibility issues with future versions of the designer.
Using this approach you and your team need to have advanced knowledge in programming, especially in JavaScript, [Typescript](https://www.typescriptlang.org) and NPM.
Also it's helpful to have some knowledge in
[Vue.js](https://vuejs.org),
[Tailwind CSS](https://tailwindcss.com),
[fabric.JS](http://fabricjs.com) and
[Vite](https://vitejs.dev)

For this approach it's required to download the source code of the designer frontend and/or backend. You can
implement your own plugins which will modify the functionality of the designer then. Finally you have to re-compile the
designer source code including your plugins, upload the compiled files to your server and configure your shop plugin configuration
to use the _customized compilation files_ instead of the original ones bundled with the shop plugin.

Please mind: The recompilation is just needed to have your plugins bundled and compiled into the output files. Using this
approach you don't modify the original source code files - you basically just use dependency injection to replace some of
their logic.

## Source code modifications

Of course it's possible to directly modify the original source code and compile it again - so this is an option, too.
You could use this approach if you don't care about being compatible to future updates and you don't want to be forced into
the DI architecture the _source code plugin approach_ requires.
In general we don't recommend touching the source code directly - but, if you were thinking about writing your own
product designer from scratch and you just use our product designer as a foundation to save time and money this could be a legit way.
