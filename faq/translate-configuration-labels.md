---
nav_order: 200
parent: FAQ
---

# How do I translate configuration labels?

First specify a _fallback_ configuration label:
![Configuration label input](/img/label-input.png)

Now add a new translation in your webshop administration for each language.
The translation key has to be:\
"kilb-product-designer.frontend.configurationLabel._Your fallback label with spaces replaced by underscores_."

So, if your fallback label is _Front Side_, the translation key has to be:\
**kilb-product-designer.frontend.configurationLabel.Front_Side.**

## Shopware

Click on _Settings_ > _Shop_ > _Snippets_.
Click the three dots icon near the translation set you want to add the translation for, then click _Edit_.
Now click on _New snippet_ and add the translation key as _Name_.

Make sure you added the translation for every translation set you use.
Please make also sure that you cleared the caches afterwards.

![Configuration label translation](/img/label-translation.png)
