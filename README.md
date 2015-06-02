<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](http://doctoc.herokuapp.com/)*

- [CSS3 Typography Techniques](#css3-typography-techniques)
  - [Font Selection Basics](#font-selection-basics)
  - [Providing Backup Fonts](#providing-backup-fonts)
  - [Google Web Fonts](#google-web-fonts)
  - [Font Face](#font-face)
    - [Browser Support](#browser-support)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

CSS3 Typography Techniques
==========

> Learning CSS3 Typography Techniques with Tuts Plus [course](http://webdesign.tutsplus.com/courses/css3-typography-techniques).

## Font Selection Basics

Primary concern should always be _legibility_ of text.

Generally don't want more than two different fonts, and don't have fonts of the same type
(eg: two serif fonts, or two monospace fonts).
[typespiration](http://typespiration.com/) has examples of fonts that go well together.

## Providing Backup Fonts

[HTML](backup-fonts/index.html) | [CSS](backup-fonts/css/styles.css)

A _web-safe_ font is a font that most users will have installed on their system,
for example Serif fonts like Times New Roman and Georgia. Or Arial, Helvetica for sans-serif fonts.

When assigning font-family to web sites, include backup fonts even when using web-safe fonts,
just in case not 100% of users have it. Otherwise, font will default to whatever the default browser font is,
which may not be for example, a sans-serif font. For example, Chrome defaults to serif.

Font names with spaces need to be quoted in css.

```css
body, html {
  font-family: "Trebuchet MS";
}
```

To provide additional fallback fonts, provide comma separated list of font names.
Last item in list should be _generic_ font such as `sans-serif` or `serif`.

```css
body, html {
  font-family: "Trebuchet MS", Helvetica, sans-serif;
}
h1, h2 {
  font-family: Georgia, "Times New Roman", Times, serif;
}
```

## Google Web Fonts

[HTML](google-fonts/index.html) | [CSS](google-fonts/css/styles.css)

A technique for including non web-safe fonts in web sites.

[Google Fonts](https://www.google.com/fonts) is a collection of open source fonts that can be used for any purpose
(eg: web, print etc.). Fonts will render on user's browsers, even if they don't have the font installed on their system.

Can change the preview text, use Filters to narrow down the font selection,
for example, uncheck "Handwriting" if not looking for that type of font.

Change default size to smaller (eg: 14 px) when looking for font for paragraph text,
to make sure it's legible at smaller size.

Preview fonts at all sizes you plan to use them.

Add all fonts you want to use to Collection, then click "Use" button.
Then select desired styles for each font, for example: weight, bold, italic, etc.

Note the page load meter, the more fonts you use on a page, the longer it will take to load.

Copy the generated `<link...` to head section of main html page.

## Font Face

[HTML](font-face/index.html) | [CSS](font-face/css/styles.css)

Another way to embed non web-safe fonts in the page is to use `@font-face` in css.
In this case, your webserver hosts the font file (check the license includes distribution rights).

For example, given a directory structure

```
my-project
├── css
│   └── styles.css
├── fonts
│   ├── Arvo-Regular.ttf
│   └── OpenSans-Regular.ttf
└── index.html
```

css `@font-face` src url attribute references font file path relative to css file location.

```css
@font-face {
  font-family: Arvo;
  src: url('../fonts/Arvo-Regular.ttf');
}

h1, h2 {
  font-family: 'Arvo', serif;
}
```

### Browser Support

`@font-face` doesn't work in IE8. It can be used in IE9, but only recognizes `eot` (embedded open type font).
Chrome, Safari and Opera recognize `ttf` or `otf` fonts (true type fonts).

Example of IE9 support, given that you have the `.eot` file for Arvo font:

```css
@font-face {
  font-family: Arvo;
  src: url('../fonts/Arvo-Regular.ttf'), url('../fonts/Arvo-Regular.eot');
}
```

## Font Sizing

[HTML](font-size/index.html) | [CSS](font-size/css/styles.css)

### Defaults

Default font size is what browser renders when no explicit font size is set in css.
Most browsers' default font size is 16 pixels (`px`) or 12 points (`pt`).
For web, avoid using points because that's designed for print (1 point = 1/72 inch).

By default, header tags and all other (h1, h2, etc) font sizes are scaled relative to the browser default font size.

For example, given `body` and `html` font size of 16px, h1 is 32px.
But if change the html font size to 14px, h1 is 28px.

```css
body, html {
  font-size: 14px;
}
```

### Percentages

Setting 100% is equivalent to using browser default. For example, this will be effectively 16px

```css
body, html {
  font-size: 100%;
}
```

Setting 120% will make font size 20% larger than default.

(4:25)
