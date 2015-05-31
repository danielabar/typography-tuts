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
