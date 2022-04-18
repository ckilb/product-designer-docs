---
title: Version 2
nav_order: 3
has_children: true
---

# Version 2

The second major version of KILB Product Designer is a huge update introducing a lot of improvements - especially for developers.

## What's new?

### Source Code Available
- The source code of the Frontend & Backend implementation is now available for all our customers
- Add your own plugins & compile a custom build of the designer

### Improved UI & Design
- Now built with Tailwind CSS for rapid UX & UI development
- A more clean and intuitive design

### Add images with a single button
- Simplified UX: There's just one button to add/upload images

### No API key required
- No need to enter an API key anymore
- Shopware's API authentication will be used instead

### Improved customizability
- Custom JS/CSS via configurations is still supported and recommended for most customers
- Custom JS can now access Vue.js store for even better customizability
- If you want to make deeper changes to the compiler you can now implement your own plugins and compile the designer for yourself

### Better API Communication
- Communication with shop server will now use GraphQL protocol
- This means less requests and a standardized way of communication

### Updated Dependencies
All the JavaScript dependencies were updated to it's newest version, most notably:
- fabric.JS: from version 3 to version 5
- Vue.js: from version 2 to version 3, using Composition API now
  Code Cleanup
- Strict code style rules were added and will be automatically checked by ESLint
- Vue.js components were split into many and are now way more light weight
- New business code layer to share logic between components

### Automated tests
- Integrated Cypress.io for automated acceptance tests
