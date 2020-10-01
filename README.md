# reset.css

A complete and modern CSS reset.



## Introduction

This style sheets completely resets all properties to the value that they would have had if no user agent or user style sheets were present. This means, that all elements look the same since they are completely unstyled. This is a great starting point for building Web applications, but will require to manually style any element that is used, including elements like `<video>`, `<input>`, `<button>`, etc.

The reset is achieved by using the CSS property `all` combined with the global value `unset` and the universal selector. Since the universal selector has no specificity, any declaration in an author style sheet will overwrite it without problems. Also this doesn't change the cascade, meaning if the user agent or user style sheet use an `!important` declaration it won't be reset.

Note: This is not a normalise style sheet, since it doesn't preserve any user agent default styles, like [normalize.css](https://github.com/necolas/normalize.css) or [destyle.css](https://github.com/nicolas-cusan/destyle.css).



## Features

- Complete reset
- Hide `<head>`, `<meta>`, `<title>`, `<link>`, `<style>`, `<script>` elements
- Focus outline for accessibility on every focusable element, even for `<html>`, `<body>`, `<embed>`, `<iframe>`, `<object>`, also customisable via `--focus-outline-width` and `--focus-outline-color` custom properties
- Border box as sizing box, instead of content box
- Flex Layout as default layout, instead of Flow Layout
- `<html>` element default size is viewport size, instead of height being only content height
- `<body>` element aligned to cross axis start to make children not stretch over full viewport



## Browser support

This reset should work in all modern browsers newer than IE11.

For more details, see browser support for [`all` property](https://caniuse.com/css-all), [CSS variables](https://caniuse.com/css-variables), and [Flexbox Layout](https://caniuse.com/flexbox).



## Roadmap

- focus outline should only show on keyboard focus instead of mouse focus, but [`:focus-visible`](https://caniuse.com/css-focus-visible) selector is not yet supported as of October 2020