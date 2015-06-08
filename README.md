<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](http://doctoc.herokuapp.com/)*

- [CSS3 Typography Techniques](#css3-typography-techniques)
  - [Font Selection Basics](#font-selection-basics)
  - [Providing Backup Fonts](#providing-backup-fonts)
  - [Google Web Fonts](#google-web-fonts)
  - [Font Face](#font-face)
    - [Browser Support](#browser-support)
  - [Font Sizing](#font-sizing)
    - [Defaults](#defaults)
    - [Percentages](#percentages)
    - [em](#em)
    - [rem](#rem)
    - [Recommendations](#recommendations)
  - [Spacing for Legibility](#spacing-for-legibility)
    - [Letter Spacing](#letter-spacing)
    - [Line Spacing](#line-spacing)
    - [Line Width](#line-width)
  - [Text Color](#text-color)
  - [Callouts](#callouts)
  - [Emphasizing Text](#emphasizing-text)
  - [Small Caps](#small-caps)
  - [Text Alignment](#text-alignment)
  - [Using Lists](#using-lists)
  - [Text Decoration](#text-decoration)
  - [Text Overflow](#text-overflow)
  - [Text Shadows](#text-shadows)
  - [Summary](#summary)

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

Setting 120% will make font size 20% larger than default, or 80% will make it smaller.

Using percentages is a powerful technique, especially for mobile,
because the default font size on mobile browsers could be different than the default font size on desktop browser.

### em

`1em` is equivalent to 100%, so it functions like a ratio. For example, this would render as the default size

```css
body, html {
  font-size: 1em;
}
```

To make the text proportionally smaller, set for example `.8em`

Issue with em units is that they're relative to _parent_ element,
so nested tags of the same type can end up getting smaller and smaller text. For example

```css
p {
  font-size: 1em;
}
span {
  font-size: 0.8em;
}
```

```html
<p>
  Some regular text, this will be rendered at 1em, i.e. 100% of the default browser font size.
  <span>
    This will be 0.8em because of the span rule defined above, so 20% smaller than its parent <p>.
    <span>
      Uh oh, this is 20% smaller than the already 20% smaller of the parent span, because that's how ems work,
      relative to parent.
    </span>
  </span>
</p>
```

### rem

Root em, solves the proportional nesting issue of ems.
All sizes are relative to the _root_ of the document instead of relative to the _parent_ element.

### Recommendations

So many different ways to size font, which to use?

Many designers recommend using [percentage](#percentages) for the body,
then use [em](#em) or [rem](#rem) for everything else.

## Spacing for Legibility

[HTML](spacing/index.html) | [CSS](spacing/css/styles.css)

### Letter Spacing

Some fonts at a small size look a little cluttered and get hard to read.
Use `letter-spacing` to space out the individual characters.
For consistency, use same units as whatever is specified for `font-size`.

```css
p {
  font-size: .9em;
  letter-spacing: 0.1em;
}
```

### Line Spacing

For some fonts, default spacing between lines is not enough to make it legible.
This can be increased via css to make it more pleasant to read.

```css
p {
  line-height: 1.6em;
}
```

Note that `line-height` is not a measure of the space between the lines,
but rather a measure of the height of the line itself.
Therefore setting it to the same value as the text size will make the lines bump up against each other.

For optimal legibility, set `line-height` to at least a little bit more than `font-size`.

### Line Width

Not good to have line go on too wide across screen, because when user has to go to next line, could skip a few.

This is controlled by applying a `width` on the container element, rather than individual paragraph elements.

```html
<div class="container">
  <p>Content here...</p>
  <p>More content...</p>
  etc...
</div>
```

```css
.container {
  width: 72em;
}
```

Note width can be set in em units if you know exactly how characters you want each line to take up.
But typically want more control over width of container, eg `width: 500px`

Lines that are too narrow are also hard to read cause the eyes have to dart back and forth too quickly.

## Text Color

[HTML](text-color/index.html) | [CSS](text-color/css/styles.css)

Color can be used to enhance or alter the _visual hierarchy_ of a site.

Some content is more important than others. Color can be used to make some text stand out or step back.

For example, to make sidebar content recede into the background a little (so it doesn't compete with main content),
could change color from black to a medium grey, given that main content is black on white.

```css
.sidebar p {
  color: #888;
}
```

Another option is to reduce the contrast between foreground and background colors of content that should be de-emphasized.
This reduces the _visual weight_ of the content.

```css
.sidebar {
  background-color: #999;
}
.sidebar p {
  color: #666;
}
```

## Callouts

[HTML](callouts/index.html) | [CSS](callouts/css/styles.css)

A callout can be used to apply _visual weight_ to a piece of text.
Often used in magazine or news articles, for exmple, to emphasize a quote.

Technique is to make a copy of the sentence and make it stand out in a _callout_.

```html
<p>Some long text here yada yad Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Make this sentence standout with a callout. Quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.<p>
<p class="callout">Make this sentence standout with a callout</p>
<p>More regular text here...</p>
```

```css
.callout {
  box-sizing: border-box;
  background-color: #ddd;
  font-size: 1.2em;
  line-height: 1.3em;
  width: 208px;
  float: left;
  margin: 0 10px 10px 0;
  padding: 10px;
}
```

## Emphasizing Text

[HTML](emphasizing-text/index.html) | [CSS](emphasizing-text/css/styles.css)

Another way to add _visual weight_ to certain pieces of text is to use `font-style` and `font-weight`.

HTML tags `<strong>` and `<emphasis>` can be used to make text bold and italic respectively.

Using these tags can break up long text by reducing the visual monotony, and create some visual interest.

Using bold text to highlight key sentences in article can help readers that are in a hurry skim through it.

Can also style text as italic or bold with css. For example

```css
.callout {
  font-style: italic;
}
```

or

```css
.callout {
  font-weight: bold;
}
```

Can also style the `<strong>` and `<em>` tags with css to make them look different than default browser behaviour.

For example, to make `strong` not bold, but instead larger and a different color:

```css
strong {
  font-size: 1.3em;
  color: rgb(218, 51, 101);
  font-weight: normal;
}
```

To make `em` not italic, but instead have a grey background color:

```css
em {
  background-color: #eee;
  font-style: normal;
}
```


Do NOT use deprecated `<bold>` and `<italic>` tags. Those have been deprecated in favour of
`<strong>` and `<em>` tags respectively because they're more semantic.

## Small Caps

[HTML](small-caps/index.html) | [CSS](small-caps/css/styles.css)

CSS property `font-variant` that applies small caps to text. For example

```html
<h3 class="subtitle">When it comes to typography in design, every decision you make has consequences.</h3>
```

```css
.subtitle {
  font-variant: small-caps;
}
```

This makes regular capital letters larger, and the other letters in capitals as well, but a little smaller.

When used with a serif font, gives an "old style" newspaper look.

## Text Alignment

[HTML](text-alignment/index.html) | [CSS](text-alignment/css/styles.css)

Most of the time, text is aligned to the left, especially for paragraphs and long blocks of text.

But for headings, or "call to action" text inside of a button, may want to center it.

```html
<h1 class="header-text">CSS3 Typography Techniques</h1>
```

```css
.header-text {
  text-align: center;
}
```

In general, centered text looks good if it's all on one line, example a heading.
Or if it's two or three lines, and they're all close to or equal in length.
Otherwise, it gets difficult to read.

To right align text, for example, to make a block quote stand out in a different way

```html
<blockquote>Some text to stand out yada yada...</blockquote>
```

```css
blockquote {
  background-color: #eee;
  padding: 10px;
  border-right: 10px solid #ddd;
  text-align: right;
}
```

## Using Lists

[HTML](lists/index.html) | [CSS](lists/css/styles.css)

* Another technique for breaking up the monotony of a long text page
* Help reader skim through the document to find what they're looking for
* Organize the content in a way that makes sense, makes the article seem more coherent

Doesn't necessarily mean adding ordered or unordered html list tags.
Could be simply adding small headers before each main paragraph of the content.

```html
<h3 class="section-header">1. This is the title of the first section</h3>
<p>Some body content blah blah...</p>
<p>Could be more stuff here...</p>
<h3 class="section-header">2. This is the second of the first section</h3>
<p>Some more body content blah blah...</p>
```

```css
.section-header {
  margin-top: 30px;
}
```

Use html `<ol>` or `<ul>` tags for lists of content. For example if article provides step by step instructions how to accomplish some task.

```html
<p>In order to create a wreath, you need to purchase the following items:</p>
<ul>
  <li>One wreath frame</li>
  <li>Some burlap</li>
  <li>One quart of burlap glue</li>
  <li>One bow</li>
</ul>
```

The unordered list can be styled to make it fit in with the rest of the body text better, for example

```css
ul {
  margin: 10px 0 10px 20px;
}
```

## Text Decoration

[HTML](text-decoration/index.html) | [CSS](text-decoration/css/styles.css)

`text-decoration` property is used to underline, overline or strikethrough.
Default value is `none`. For a link, default value is `underline`.

Keep in mind user's expectations. For example, if text is underlined, most users will assume it's clickable.
Therefore don't underline text unless it actually is a link or you have a really good reason to do so.

For example, to put a line over the text

```html
<p>
  Some paragraph text...
  <span class="decorate">this text should be decorated</span>
  more paragraph text
</p>
```

```css
.decorate {
  text-decoration: overline;
}
```
Overline not used very often. One example usage could be to change appearance of link when hovered over

```css
a:hover {
  text-decoration: overline;
}
```

Another text-decoration value is `line-through` which creates a strikeout effect.

```html
I <span class="decorate">like</span> love typography.
```

```css
.decorate {
  text-decoration: line-through;
}
```

Can also set `text-decoration` to `none` to remove default browser styling for anchor tags,
for example, if its being styled as a button and is otherwise very obvious that it's clickable,
then the underline is not needed.

## Text Overflow

[HTML](text-overflow/index.html) | [CSS](text-overflow/css/styles.css)

For example, say you have a container that displays the most recent blog posts, which are pulled from a CMS or database.
You don't know in advance how big that text will be. Can change the way the text behaves when it _overflows_ its container div.

For example, to cut off the paragraphs at container width and show "..."

```html
<ul class="blog-list">
  <li><h4>Blog Title 1</h4>
    <p> Some really long text</p>
  </li>
  <li><h4>Blog Title 2</h4>
    <p> Some more really long text</p>
  </li>
</ul>
```

```css
.blog-list p {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
```

## Text Shadows

[HTML](text-shadows/index.html) | [CSS](text-shadows/css/styles.css)

First two values for `text-shadow` are the horizontal and vertical positions of the shadow.
Third value is blur distance (optional), and fourth value is shadow color (also optional).

To make a text shadow that is 2px to the right of the text, 3px down from the text, 4px of blur distance, and light grey:

```css
.header-text {
  text-shadow: 2px 3px 4px #bbb;
}
```

Watch out: Don't get `box-shadow` and `text-shadow` mixed up. Box shadow applies to a div container,
whereas text shadow applies to individual letters.

## Summary

Typography is in part an art form, and somewhat subjective. However, a few key rules to keep in mind:

* Provide an easy and pleasant reading experience
* Only use one or two different types of fonts in a given design, any more may look clutterred and indecisive
