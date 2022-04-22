---
nav_order: 3
parent: FAQ
---

# Is it possible to add or remove fonts?

By default the product designer ships with several popular fonts which should be sufficient for most.
Still, if you like you can use your own list of fonts the customer can choose from.

**Please mind** that there's no support from our side for your own fonts. If one of your fonts doesn't work as expected you probably cannot use it.

After you successfully set up the product designer and created a configuration for one of your articles you will find a new directory 
`Product Designer - Fonts` inside the media manager in the backend of your shop system.
If you place at lease one file here your own fonts will be used. If you remove all the files in the directory - so the directory is empty -the default fonts shipped with the designer will be used again.
Please mind that only fonts will be used if the following requirements are met:

- it's a valid *TTF* font
- the extension of the file is exactly `.ttf`
- there's only numbers and letters in the file name - no other characters are allowed
- the first character of the file name must be an upper case letter (A-Z)
- file names of fonts in bold type end with `-Bold.ttf`. If there's no file for the bold type existing the customer can't set the text to bold for this font.
- file names of fonts in italic type end with `-Italic.ttf`. If there's no file for the bold type existing the customer can't set the text to italic for this font.
- file names of fonts in bold & italic type end with `-BoldItalic.ttf`. If there's no file for the bold & italic type existing the customer can't set the text to both bold & italic for this font.

Some examples for valid file names are:

`Audiowide.ttf`
`OpenSans.ttf` (not: `OpenSans-Regular.ttf`)
`OpenSans-Bold.ttf`
`OpenSans-Italic.ttf`
`OpenSans-BoldItalic.ttf`

You can find a lot of usually well-supported fonts on [Google Fonts](https://fonts.google.com).
Please mind that you have to download the fonts from there and upload them to your media manager again like described above.
The product designer will **not** load the fonts directly from Googles servers so there won't be any issues privacy-wise and GDPR.
