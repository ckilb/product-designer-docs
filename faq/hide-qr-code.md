---
nav_order: 200
parent: FAQ
---

# How can I remove the QR code button?

The simplest way to do that is to create some CSS file with the following content:

`custom.css`

```css
[data-component="action.qr-code-button"] { display: none; }
```

Now upload that CSS file to your shop server in a directory which is publicly available.
For Shopware this is usually the directory `shopware-installation-path/public/` so the file path would be:

`shopware-installation-path/public/custom.css`

Now get the URL to the CSS file, for instance
`https://your-shop.de/custom.css` and add this CSS file to your product designer configuration (*Advanced* Tab).

Read more about what you can do with this kind of customizations here:
[Monkey Patching](/customizations/monkey-patching.html)
