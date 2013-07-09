Media Queries to Media Types with LESS
======================================

Turn this... `@media all and (min-width:768px) { ... }` into this... `@media all { ... }`

A method for creating an [IE specific stylesheet](http://css-tricks.com/how-to-create-an-ie-only-stylesheet/) that allows the content of media queries to become accessible to Internet Explorer 8 and below. This process uses [LESS string interpolation](http://lesscss.org/) to convert media queries into [media types](http://www.w3.org/TR/CSS2/media.html) which are [supported back to IE6](http://msdn.microsoft.com/en-us/library/hh781508.aspx#at-rules).

This is especially useful if you write mobile-first styles and inline (scatter) your media queries instead of writing them in one big block in a separate file.

---

**OR** if you're using grunt.js then [here is a simple way to strip mobile-first media queries](https://github.com/jtangelder/grunt-stripmq).

---

## Documentation

```
// vars.less
// Examples of using LESS's string interpolation to turn your
// media queries into variables.
@respond-to-medium-screens: "all and (min-width: 600px)";
@respond-to-medium-screens-max: "all and (max-width: 599px)";
@respond-to-large-screens: "all and (min-width: 768px)";
@respond-to-large-screens-max: "all and (max-width: 767px)";

// vars-ie-overrides.less
// Used only to override any media queries that affect the "desktop" layout
@respond-to-medium-screens: "all";
@respond-to-large-screens: "all";

// base.less
// Write styles as usual but when writing your media queries
// use the variables you set up: `@media @respond-to-large-screens`
@media @respond-to-medium-screens { ... }
@media @respond-to-large-screens { ... }

// styles.less
// This stylesheet will pull everything together and your
// media queries will be compiled as normal: `@media all and (min-width: 768px)`
@import "vars.less";
@import "base.less";

// styles-ie.less
// This stylesheet is for IE8 and below and also pulls everything together
// except that it uses vars-ie-overrides.less to override any media queries that
// affect the "desktop" layout. Your media queries will now be converted to media
// types and will look like this: `@media all`
@import "vars.less";
@import "vars-ie-overrides.less";
@import "base.less"; // This is the same file as above
```

All that's left is to serve **styles-ie.css** to IE8 and below like so.

```html
<!--[if lt IE 9]>      <link rel="stylesheet" href="styles/styles-ie.css"> <![endif]-->
<!--[if gt IE 8]><!--> <link rel="stylesheet" href="styles/styles.css"> <!--<![endif]-->
```

## Contributing

Discussion is welcome using github issues

- [Testing different media types](https://github.com/himedlooff/media-query-to-type/issues/1)

## Spreading the word

Curating a list of sites I'm using to spread the idea and collect feedback.

- [less.js pull #643](https://github.com/cloudhead/less.js/pull/643)
- [less.js issue #965](https://github.com/cloudhead/less.js/issues/965)
- [nicolasgallagher.com - “Mobile first” CSS and getting Sass to help with legacy IE](http://nicolasgallagher.com/mobile-first-css-sass-and-ie/#comment-94783) (awaiting comment moderation)
- [coding.smashingmagazine.com - Techniques For Gracefully Degrading Media Queries](http://coding.smashingmagazine.com/2011/08/10/techniques-for-gracefully-degrading-media-queries/comment-page-1/#comment-944717)
