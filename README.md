Media Queries to Media Types with LESS
======================================

Turn this... `@media only screen and (min-width:768px) { ... }` into this... `@media screen { ... }`

A method for creating an [IE specific stylesheet](http://css-tricks.com/how-to-create-an-ie-only-stylesheet/) that allows the content of media queries to become accessible to Internet Explorer 8 and below. This process uses [LESS string interpolation](http://lesscss.org/) to convert media queries into [media types](http://www.w3.org/TR/CSS2/media.html) which are [supported back to IE6](http://msdn.microsoft.com/en-us/library/hh781508.aspx#at-rules).

This is especially useful if you write mobile-first styles and inline (scatter) your media queries instead of writing them in one big block in a separate file.

## Getting Started

Set up LESS, I'm using [Recess, a grunt plugin](https://github.com/sindresorhus/grunt-recess)

## Documentation

```
//styles.less
@import "vars.less"; // This contains: `@respond-to-large-screens: ~"only screen and (min-width: 768px)";`
@import "base.less"; // Write styles as usual but when writing large-screen media queries write them like this `@media @respond-to-large-screens`

//styles-ie.less
@import "vars-ie-overrides.less"; // This contains: `@respond-to-large-screens: ~"screen";`
@import "base.less"; // This is the same file as above
```

When compiled the two files will treat `@media @respond-to-large-screens` differently.

**styles.less** will output `@media only screen and (min-width: 768px)`

**styles-ie.less** will output `@media screen`

All that's left is to serve **styles-ie.css** to IE8 and below like so.

```html
<!--[if lt IE 9]>      <link rel="stylesheet" href="styles/styles-ie.css"> <![endif]-->
<!--[if gt IE 8]><!--> <link rel="stylesheet" href="styles/styles.css"> <!--<![endif]-->
```

## Contributing

Discussion is welcome using github issues

