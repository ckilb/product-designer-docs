---
parent: Customizations
nav_order: 1
---

# Source Code

## Architecture

The product designer basically consists of three parts.

### Shop integration & API provider
This is mostly implemented in PHP.
You can find the source code for this if you have a look into the *plugin installation directory* of you online shop.
For Shopware it's `custom/plugins/KilbShopwareProductDesigner`.
There's no public repository for this. If you want to change the logic here you should create your own plugin 
which will replace or extend the designer plugin. 
You will get an idea of how this works in the developer documentation of your online shop system.

The shop integration will extend your online shop's templates to add *iframes* which will load the Frontend and Backend of the designer.

### Frontend
This is the actual implementation of the designer and most parts are implemented in TypeScript.
Because of using TypeScript the source code has to get compiled.
The compilation will consists of several asset files. One of them is an *index.html* file which will be loaded by the shop integration via *iframe* on the product detail page.

### Backend
This is the implementation of the designer's backend and most parts are implemented in TypeScript.
Because of using TypeScript the source code has to get compiled, too.
The compilation will consists of several asset files. One of them is an *index.html* file which will be loaded by the shop integration via *iframe* in the administration area.

## Get the source code

To get the source code you need to have `git` installed. 
You are able to clone the repositories then. You can also update your cloned repository files via `git pull` from time to time.

`git clone http://sources.product-designer.io/product-designer-backend.git`

`git clone http://sources.product-designer.io/product-designer-frontend.git`

`git` will ask your for a username and password.
You will find both at the bottom of the *Documentation* page in the administration area of your product designer installation.
Please keep the credentials and the source code confidential. You are only allowed to work with it in a production system after you've purchased the plugin.
You are only allowed to update the source code if you have an active subscription.

