Spread
===========

## Initial Setup 
Spread is dependent on [Ruby](https://www.ruby-lang.org/en/) and [Compass](http://compass-style.org/). Installation instructions [here](http://compass-style.org/install/).

 1. Install [ruby](https://www.ruby-lang.org/en/installation/#installers)
	 - `ruby-install ruby`
 2. Install [compass](http://compass-style.org/install/)
	 - gem update --system 
	 - gem install compass
 4. Install our compass dependencies: [import-once](https://github.com/livereload/livereload-plugins/tree/master/SASS.lrplugin/gem/gems/compass-import-once-1.0.1) `gem install compass-import-once`
 5. Run `compass compile` on the command line to convert from SASS to CSS
 6. Run `compass watch` to compile automatically on save.
 7. Open up `index.html` for further details and usage!

### Golden Gridlet

This is an excellent tool developed by the amazing [Joni Korpi](http://jonikorpi.com/), inventor of the [Golden Grid System](http://www.goldengridsystem.com). You can click the little hamburger icon in the upper-right of the screen to get an accurate display of the current column layout with gutters and baselines. The default settings can be manipulated in the `GGS.js` file.

## Layout Functionality

### Column Layout

#### DIV Hierarchy

There's a pre-established structure for layout, from highest to lowest level. Any kind of modifications would simply be nested SASS classes pertaining to these structural elements. The structure is fairly simple, and goes in this order:

1. `wrapper`
2. `columns-#` (Column Layout)
3. `column`
4. `gutter-pad`

####Wrapper
Offers a 5.5555% padding on either side, also offers space for a full background color or image. A containing DIV is sometimes used for organization.

####Column Layout `(columns-x)`
You can utilize the columns by generating layouts. There's a Sass mixin built in that does all the calculations for you, including `offset-x` and `wide-x` classes! Just call the mixin by using: `@include column-calculator(x)` Where X is the number of columns you want. Each column layout e.g. `columns-2`, `columns-4`, etc., exists solely to give style context to a `column` div.

*Pro-tip: The `column-calc` mixin currently only supports column layouts divisible by 2.*


####Columns

A column's width is the resulting percentage 100 divided by the number of columns inputted. For example, the width of a `column` in a `columns-4` layout evaluates to `width: 25%`. A nested `gutter-pad` class offers a horizontal padding of `0.75 em`s for typography, totalling `1.5 em`s of gutter between columns.

####Wides

This same calculation is applied to `wides`, but then multiplied by however many columns wide you'd like the div to be. For example, the width of a `column wide-3` div in a `columns-4` layout evaluates to `width: 75%`.

####Offsets

Lastly, an offset is the displacement of a `div` by a specified number of columns using a simple `margin`. For example, the `margin-left` of a `column offset-2` in a `columns-4` layout is `margin-left: 50%`.

###Column Behavior

The `+column-calc` mixin includes media queries for different viewport sizes, as well as behavioral degradation for column-widths, wides, and offsets. For example, a 16-column layout will become 8-column at a tablet screen size, then 4-column on a mobile screen size. The threshold for these screen sizes is set in the `_variables.sass` file. 

There are 4 tiers:

 1. `width-mobile` : 320px
 2. `width-tablet` : 640px
 3. `width-desktop-small` : 1280px
 4. `width-desktop-large` : 2560px

These variables can be redefined according to taste and necessity, but the behavior can be altered as well in the `_column-calc.sass` file. If you've got a decent understanding of functions in SASS, you'll find that it's fairly straightforward. Each set of behavioral rules are nested inside of media queries with screen sizes determined by the variables mentioned above.


###[Vertical Rhythm](http://compass-style.org/reference/compass/typography/vertical_rhythm/)


In order to properly align to the baseline grid as shown in the Golden Gridlet, `font-size` and `line-height` must be specified in proportionate `em`s. An "em" in the world of typography is the size of a capital M in reference to a specified font size. One em in a `body` with a specified `font-size: 16px` is, in fact, 16px. This allows for a proportionally relative typography system throughout an entire project.

There are a pair of beautiful Compass mixins that accomplish this concept wonderfully.

####`@include adjust-font-size-to (16px,1)`
- The first argument can be either a pixel value or a previously defined variable.
- The second argument is the line height expressed in baselines. You can visualize these baslines using the Golden Gridlet. 
- These two arguments are used to calculate the `font-size` and `line-height` into `em`s.
 
####`@include rhythm (0,1,1,0,16px)`
This mixin specifies vertical margin and padding in the following order:

1. margin-top
2. padding-top
3. padding-bottom
4. margin-bottom
5. Current font size (if specified) 

These arguments should be specified as whole numbers, as they're the same baseline units used to specify line-height in the font mixin.

*Pro-tip: It's a good idea to give all elements a reset of `+rhythm(0,0,0,0)` to keep things adhered to the baseline grid, even if they don't have any vertical padding or margin.*

###That's All, Folks!

This system is just a starting point. If you need to tailor it to your application or content, please do so. A grid system is only valuable if it helps to display your content and how it behaves on different devices. It's a **response** to the question of "how will this look on mobile?", but it's up to you how to make it **the answer**.