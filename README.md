# Typecsset (v0.3.0)

**<cite>Typecsset</cite> (type·set, /ˈtīpˌset/) is a small Sass library for
setting type on the web.**

It gives you an automatic, pixel-perfect, baseline grid across all textual HTML
elements based entirely on just a few settings of your choice. Baseline grids
without the headaches.

## Demo

* [View demo](http://csswizardry.com/typecsset/)
* [View demo code](https://github.com/csswizardry/typecsset/tree/gh-pages)

## Implementation

Using Typecsset couldn’t be easier. Download the Sass file, predefine any
settings, `@import` it into your project, _go!_

```scss
$typecsset-base-font-size:      18px;
$typecsset-base-line-height:    27px;

[Your own CSS]

@import "path/to/typecsset";

[More of your own CSS]
```

**[Example](https://github.com/csswizardry/typecsset/blob/gh-pages/style.scss)**

### Precision

Due to the nature of unitless and relative values, you will end up with a lot of
floats as opposed to integers (e.g. `line-height: 1.333;` instead of
`line-height: 24px;`). In order to ensure that browsers can work these values
out as closely as possible to the pixel, thus avoiding rounding errors, I
recommend compiling your Sass with the `--precision` flag set to `7`, e.g.:

    sass --watch typecsset.scss:typecsset.css --style expanded --precision 7

## Settings

All Typecsset’s settings are stored in namespaced variables (e.g.
`$typecsset-base-font-size`). You should avoid modifying these directly, as to
do so would inhibit your ability to smoothly update the library. If you would
like to modify the default settings in Typecsset, predefine them _before_ you
import the library, as above.

There are certain settings in Typecsset that should not and cannot be
overridden, as they are fundamental to the way the library works. These settings
are, however, based upon the settings you _can_ modify.

### `$typecsset-base-font-size`

This is the base font size you would like your project to have. Set this in
pixels: Typecsset will convert it to the relevant units for you.

### `$typecsset-base-line-height`

This is the base line height you would like your project to take. Again, define
this in pixels: Typecsset will convert it into a unitless value for you.

This `$typecsset-base-line-height` value is the most important one in the whole
library - it defines and underpins your whole vertical rhythm. Everything
(`margins`, `line-height`s, etc.) will be based upon units of this number in
order to maintain a consistent and harmonious vertical rhythm.

### `$typecsset-h[1-6]-size`

These settings, predictably, contain the desired font sizes for your headings
one-through-six. Again, they are set in pixels because the library will pick
them up and convert them into rems later on. *For automatic settings, see below.*

### `$typecsset-auto-scale`

This is a boolean toggle to allow your headings to be automatically scaled based on a modular scale. This is based on the principles outlined by [Tim Brown's aricle, "More Meaningful Typography"](http://alistapart.com/article/more-meaningful-typography).

### `$typecsset-ratio`

If you set `$typecsset-auto-scale = true`, you can also set the ratio at which your headings scale. The value of this can either be a list of two numbers (typically based on [musical intervals](http://en.wikipedia.org/wiki/Interval_(music\)) ) or a float(1.33). The default is 4,3 (a perfect fourth). See [Tim's aricle](http://alistapart.com/article/more-meaningful-typography) for some more useful intervals.

*Note: 3,4 and 4,3 would result in the same scale. This is because Musical intervals are sometimes written in either order and a sub 1 scale would be fairly useless.*

### `$typecsset-indented-paragraphs`

This is a simple boolean to toggle between indented—as you traditionally find in
print—or simply spaced—more common on the web—paragraphs.

### `$typecsset-show-baseline`

Another boolean which will simply turn a baseline grid either on or off. The
image used for the grid is provided by [Basehold.it](http://basehold.it/), and
is based on the value of `$typecsset-base-line-height`. It will automatically
update itself whenever you modify the value of `$typecsset-base-line-height`.

### `$typecsset-magic-number`

This is a library setting, and cannot/should not be modified. Your _magic
number_—typographically speaking—is the number which underpins your vertical
rhythm. This is sourced from your `$typecsset-magic-number` setting and will
define the `margin`s and `line-height`s for all typographical elements.

### `$typecsset-magic-ratio`

This is another library variable, and simply holds your magic number as a ratio
of your chosen base font size.

## Tools

Typecsset has a number of mixins and functions which are used to generate more
verbose CSS around your own settings.

### `typecsset-font-size()`

This mixin takes a pixel value for a font size and converts it into a
rem-with-pixel-fallback `font-size`, with a unitless `line-height` based upon
your vertical rhythm. Clever stuff!

**Input:**

```scss
$typecsset-base-font-size:      16px;
$typecsset-base-line-height:    24px;

[...]

.foo {
    @include typecsset-font-size(20px);
}
```

**Output:**
```css
.foo {
    font-size: 20px;
    font-size: 1.25rem;
    line-height: 1.2;
}
```

* `font-size: 20px;`: A pixel fallback simply lifted straight from the input
  into the mixin.
* `font-size: 1.25rem;` A rem-based font-size for supporting browsers. This is
  calculated by _desired font-size_ / _base font-size_ = _font-size in rems_.
  20 / 16 = 1.25.
* `line-height: 1.2;`: This is a unitless value greater than 1 which, when
  multiplied by the element’s font-size, yields a number that is a multiple of
  your base line-height. It is this which keeps everything on your baseline.
  1.2 * 20 = 24px.

### `typecsset-space()`

The `typecsset-space()` mixin simply drops a double amount of ‘spacing’ onto a given
property, e.g. `padding`:

**Input:**

```scss
$typecsset-base-line-height:    24px;

.foo {
    @include typecsset-space(margin-bottom);
}
```

**Output:**

```css
.foo {
    margin-bottom: 48px;
    margin-bottom: 3rem;
}
```

This simple-looking mixin just DRYs out some repeated Typecsset functionality.

### `typecsset-strip-units()`

The `typecsset-strip-units()` function simply does as it says: it removes the
units from a value that is passed into it:

**Input:**

```scss
.foo {
    line-height: typecsset-strip-units(1.5px);
}
```

**Output:**

```css
.foo {
    line-height: 1.5;
}
```

This very useful function only gets used once—to get us our baseline grid image:

```scss
[...]

$typecsset-baseline-size: typecsset-strip-units($typecsset-magic-number);

background-image: url(http://basehold.it/i/#{$typecsset-baseline-size}); /* [3] */

[...]
```

### `typecsset-scale()`

This mixin takes a value and a property as in input and gives you a pixel and rem value based on your modular scale. The first value represents from where on your scale you want to pull.

**Input:**

```scss
$typecsset-base-font-size:      16px;
$typecsset-base-line-height:    24px;
$typecsset-auto-scale:          true;
$typecsset-ratio:               4,3;

[...]

.foo {
    @include typecsset-scale(1, margin-left);
}
```

**Output:**

```css
.foo {
    margin-left: 21.3333px;
    margin-left: 1.3333rem;
}
```

As an added bonus, you can go down your scale as well by using negative numbers.

*Note: If font-size is used, line-height will also be included*