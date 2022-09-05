# reset.css

A complete CSS reset and a modern default style



## Introduction

Tired of battling browser styles? Tired of mixing your styles with browser unset styles? Tired of writing `margin: 0;` all the time? Enter `reset.css`. This style sheets completely resets all properties to the value that they had if no user agent or user style sheet were present. In an ideal world browsers would not have styled by default (and each one slightly differently!). Now, thanks to the recent CSS property `all` living in an ideal world becomes possible.

Note, all elements will look the same by default since now they are completely unstyled. You will have to style any element that you use, including commonly used elements like `<video>`, `<input>`, `<button>`, etc. whose looks up until now you might have taken for granted. It might take you longer to get started but it will pay off in the long run!

Note, this is not a normalise style sheet, since it doesn't preserve any user agent default styles, unlike [normalize.css](https://github.com/necolas/normalize.css) or [destyle.css](https://github.com/nicolas-cusan/destyle.css).

After resetting everything, this style sheet also includes modern default styles that are a great starting point for building Web applications.



## Features

- Reset everything
- Hide `<head>`, `<meta>`, `<title>`, `<link>`, `<style>`, `<script>` elements again
- Focus outline for accessibility on every focusable element (including `<html>`, `<body>`, `<embed>`, `<iframe>`, `<object>`), customisable via `--focus-outline-width` and `--focus-outline-color` custom properties
- Border box as sizing box, instead of content box
- Flex Layout as default layout, instead of Flow Layout
- `<html>` element default size is viewport size, instead of height being only content height
- `<body>` element default size is viewport size
- Border style as solid instead of none, border width as none instead of medium, such that can add solid border just by setting its width



## Demo

See the test page [with reset](test.html) and [without reset](testbaseline.html). Thanks to [html5-test-page](https://github.com/cbracco/html5-test-page).



## Getting started

Simply include `reset.css` in the head of your document *before* any of your own styles.



## Details

The reset uses the CSS property `all` combined with the global value `unset` and the universal selector. Since the universal selector has no specificity, any declaration in any author style sheet will overwrite it. Also it doesn't change the cascade, meaning if the user agent or user style sheet use an `!important` declaration it won't be reset. This means the reset itself can be anywhere in the document. It's recommended to include `reset.css` first because of the modern defaults.

Note, `reset.css` assumes you style from the `<body>` element downwards. For example, if you use a framework that inserts wrapper elements between your entry point and the `<body>`, you'll need to style those as well, e.g. `flex-1`.



## Browser support

This reset should work in all modern browsers. Note, the focus outline is supported in all browsers only since March 2022 when Safari finally gained support.

See CanIUse entries for [`all` property](https://caniuse.com/css-all), [CSS variables](https://caniuse.com/css-variables), [Flexbox Layout](https://caniuse.com/flexbox), and [`:focus-visible` selector](https://caniuse.com/css-focus-visible).



## Known issues

### SVG elements aren't visible or lost their styles

Styling properties of SVG elements defined as presentational attributes are reset, because they behave as if they were defined at the top of the author style sheet with specificity 0, and therefore the `all` shorthand overrules them. That presentational attributes don't behave like inline styles may not be what one expected, but is intended behavior according to the [SVG spec](https://www.w3.org/TR/SVG2/styling.html#PresentationAttributes).

> Presentation attributes contribute to the author level of the cascade, following all other author-level style sheets, and have specificity 0.

The solution is to define styling properties in CSS instead of in HTML attributes, for example in inline styles. This is anyways the recommended way of defining styling properties according to the SVG spec.

> In the future, any new properties that apply to SVG content will not gain presentation attributes. Therefore, authors are suggested to use styling properties, either through inline ‘style’ properties or style sheets, rather than presentation attributes, for styling SVG content.

Note: Don't forget to add units in CSS, as a unitless CSS value doesn't default to the pixel unit as it does for presentational attributes!

```html
<!-- HTML ATTRIBUTES 👎 -->

<svg width="100" height="100" version="1.1" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="45" stroke="red" fill="transparent" stroke-width="5" />
  
  <path d="M 10,30 A 20,20 0,0,1 50,30 A 20,20 0,0,1 90,30 Q 90,60 50,90 Q 10,60 10,30 z"/>
</svg>
```

```html
<!-- CSS PROPERTIES 👍 -->

<svg width="100" height="100" version="1.1" xmlns="http://www.w3.org/2000/svg">
  <circle style="cx: 50px; cy: 50px; r: 45px; stroke: red; fill: transparent; stroke-width: 5" />

  <path style='d: path("M 10,30 A 20,20 0,0,1 50,30 A 20,20 0,0,1 90,30 Q 90,60 50,90 Q 10,60 10,30 z")'/>
</svg>
```

beware: as of Nov 2020, the `d: path("..")` syntax isn't yet in the SVG spec and only supported by Chrome, see SVG spec [#374](https://github.com/w3c/svgwg/pull/374) and invalid Chromium bug [1134976](https://bugs.chromium.org/p/chromium/issues/detail?id=1134976).

### Color property of anchor element isn't reset in older Chrome versions

Older Chrome versions before 92 experienced a bug where they didn't apply the `all: unset` rule for the `color` property of an anchor element in some or all states. This was fixed in Chrome 92 released on July 20, 2021. Refer to the bugs [1195644](https://bugs.chromium.org/p/chromium/issues/detail?id=1195644) and previously [1195644](https://bugs.chromium.org/p/chromium/issues/detail?id=1134443).

If you need to support older Chrome versions, you can reset the `color` property manually. Add the following rule to `reset.css`.

```css
a {
    color: unset;
}
```