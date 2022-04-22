---
parent: Customizations
nav_order: 2
---

# Source Code Plugins

## Recommended tools

- **Browser**: A Chromium based web browser like Google Chrome
- **Browser extensions**: [Vue.js Devtools](https://chrome.google.com/webstore/detail/vuejs-devtools/ljjemllljcmogpfapbkkighbhhppjdbg?hl=en)
  , [Cross Domain CORS](https://chrome.google.com/webstore/detail/cross-domain-cors/mjhpgnbimicffchbodmgfnemoghjakai?hl=en) to disable CORS security checks and [GraphiQL](https://chrome.google.com/webstore/detail/graphiql-extension/jhbedfdjpmemmbghfecnaeeiokonjclb?hl=en) to test GraphQL queries.
- **IDE**:
    - IntelliJ with Vue.js and Tailwind Plugin - or
    - Visual Studio Code with [Volar](https://marketplace.visualstudio.com/items?itemName=johnsoncodehk.volar) and [Tailwind](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss) extension


## Set up the project

### 1. Get the source code
```shell
git clone git@...
```

### 2. Install [nvm](https://github.com/nvm-sh/nvm) & switch to required node version
```shell
cd ./path-to-repository && nvm install && nvm use
```

### 3. Install dependencies
```shell
npm install
```

### 4. Create & adjust iframe.html
```shell
cp iframe.html.dist iframe.html
```
Now open _iframe.html_ and
- replace ``[[[ URL TO YOUR WEBSHOP ]]]`` with the URL to your web shop you want to use for development.
- replace ```[[[ ARTICLE NUMBER ]]]``` with the number of the article you like to use for development.
- replace ```[[[ LOCALE ]]]``` with the locale code like _en-GB_ or _de-DE_ you like to use for development.

### 5. Run development server

This command will start the development server and open the designer in your browser.\
```npm run dev```

Make sure everything is working as expected. If not, check for errors and XHR responses in your browser's web developer tools.
If you get CORS issues you could install a browser extension that disable these checks. For your production
environment you should make sure domain names match or set appropriate CORS headers.

## Create a plugin

Although you are able to fork this repository and change the code of the designer wherever you like it may not be the best
option as you would lose compatibility to future updates of the designer.

Instead you could create a plugin which adjusts the components and business logic of the designer
without the need to touch even a single file shipped with the designer.

### 1. Create plugin entry point

Create a new directory inside ```./src/plugins``` and place a new file ```index.ts``` in there

```mkdir ./src/plugins/my-plugin && touch ./src/plugins/my-plugin/index.ts```

### 2. Add a default-exported initialization function inside that file

```typescript
import { DependencyContainer } from 'tsyringe';

export default function initialize(container: DependencyContainer): Promise<void> {
  return new Promise<void>((resolve) => {
    resolve();
  });
}
```

The designer will automatically load the file and calls that function with the DI container.\
You can replace Vue.js components and business facades within the container.

### 3. Replace a component

- Create your own component inside your plugin directory, for instance
  ```./src/plugins/my-plugin/MyQrCodeComponent.vue```

- Implement your component, for instance

```html
<template>
    <button @click="onClick()">My QR Code button</button>
</template> 

<script lang="ts" setup>
function onClick() {
    console.log('My QR Code implementation');
}
</script>
```

- Use the DI container to register your component.

```typescript
import { DependencyContainer } from 'tsyringe';
import MyQrCodeButtonComponent from './MyQrCodeButtonComponent.vue';

export default function initialize(container: DependencyContainer): Promise<void> {
  return new Promise<void>((resolve) => {
    container.register('action/QrCodeButtonComponent', {
      useValue: MyQrCodeButtonComponent,
    });

    resolve();
  });
}
```

- Learn more about Dependency Injection with [Tsyringe on their Github page](https://github.com/microsoft/tsyringe).

### 4. Reuse & replace business logic

Vue.js components are light weight and usually only contain a few lines of Typescript code.
Most business logic can be found in ```/src/business```. While you can replace
that code as well it's recommended to _not_ do so. Instead, create your own logic - which may use
the business logic of the designer internally - and replace the facade method.

For instance, to add your own logic to the image upload functionality,
create your own _image facade_:

`./src/plugins/my-plugin/image-facade.ts`

Content:

```typescript
import { inject, singleton } from 'tsyringe';
import { ResultAsync } from 'neverthrow';
import ImageFacade, { IImageFacade } from '../../business/image';

@singleton()
class MyImageFacade implements IImageFacade {
  constructor(
    @inject(ImageFacade) private imageFacade: IImageFacade,
  ) {}

  uploadImage(imageFile: File): ResultAsync<string, Error> {
    // add your own logic, call original logic

    return this.imageFacade.uploadImage(imageFile);
  }
}

export default MyImageFacade;
```

Use the DI container to register _your_ facade:

```typescript
import { DependencyContainer } from 'tsyringe';
import MyImageFacade from './image-facade';
import ImageFacade, { IImageFacade } from '../../business/image';

export default function initialize(container: DependencyContainer): Promise<void> {
  return new Promise<void>((resolve) => {
    const originalImageFacade = container.resolve(ImageFacade);
    const myImageFacade = new MyImageFacade(originalImageFacade);

    container.registerInstance<IImageFacade>(ImageFacade, myImageFacade);

    resolve();
  });
}
```

## Build

You can build the designer using
```npm run build```

This will create the minified, compiled output files inside ```/dist```. You can copy these files to your shop server.
Make sure the shop plugin is configured to use your _custom build_ instead of the default build shipped with the plugin.

## Used libraries & frameworks

This product designer would not have been possible thanks to a lot of Open Source libraries and frameworks.
The most import frameworks you should know about are
- [Vue.js](https://vuejs.org/)
- [Tailwind CSS](https://tailwindcss.com/)
- [Fabric.js](http://fabricjs.com/)

