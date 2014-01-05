# Typecsset

**Typecsset is a small Sass library for setting beautiful type on the web.**

* Consistent, automagic vertical rhythm.
* Proper quotes.

## Implementation

Using Typecsset couldn’t be easier. Download the Sass file, predefine any
settings, `@import` it into your project, _go!_

    $typecsset-base-font-size:      18px;
    $typecsset-base-line-height:    27px;

    [Your own CSS]

    @import "path/to/typecsset";

    [More of your own CSS]

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
library—it defines and underpins your whole vertical rhythm. Everything
(`margins`, `line-height`s, etc.) will be based upon units of this number in
order to maintain a consistent and harmonious vertical rhythm.

### `$typecsset-h[1–6]-size`

These settings, predictably, contain the desired font sizes for your headings
one-through-six. Again, they are set in pixels because the library will pick
them up and convert them into rems later on.

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
