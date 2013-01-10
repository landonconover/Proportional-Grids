# Proportional Grids

Don’t think widths, think proportions. A dead simple method of creating responsive fluid grids with fixed gutters. Use classes to set the proportions you want your columns to take at which breakpoint.

Supports nested grids and requires no `class="first"` or `:first-child` nonsense. **Even works in IE7 and below**

**[Check out the demo](http://builtbyboon.com/posed/Proportional-Grids/)** or **[Read all about it](http://builtbyboon.com/blog/proportional-grids/)**

[built by Boon](here: http://builtbyboon.com/) - given away free

If you have questions or put this to use then [hit me up on Twitter](http://twitter.com/mattberridge)

*A shout must go out to Harry Roberts ([@csswizardry](http://twitter.com/csswizardry)) for pointing me in the right direction with the idea!*

## How it works

There is no `class="first"` to add to any of your columns because the gutter on the first column has been negated like so:

	.grid-wrap {    
		margin-left: -3em; /* the same as your gutter */
		overflow: hidden;
		clear: both; }
	   
	.grid-col {
		float: left;
		padding-left: 3em; /* this is your gutter between columns */
		width: 100%;
		-webkit-box-sizing: border-box;
		   -moz-box-sizing: border-box;
				box-sizing: border-box; }

Classes are then used on each column to determine which proportion is taken at which breakpoint:

	<div class="grid-wrap">
		<div class="grid-col bp1-col-one-half bp2-col-two-thirds">
			<p>Column 1</p>
		</div>
		<div class="grid-col bp1-col-one-half bp2-col-one-third">
			<p>Column 2</p>
		</div>
	</div>

In this example, each `grid-col` starts life as a single column. The class `bp1-col-one-half` means that column becomes one-half at breakpoint 1. `bp2-col-two-thirds` means it becomes two-thirds at breakpoint 2. And so on.

It's that simple, one grid system, one set of classes, wherever you want!

`bp2-col` is simply a namespace / prefix for that breakpoint. You can call these whatever you like but I prefer to use numbers rather than being stuck to a device e.g. `tablet-col`.	

## Internet Explorer

Obviously IE8 and below does not support `@media` and IE7 and below does not support `box-sizing`. But fear not, I’ve added an IE-specific stylesheet which repeats everything that appears inside a media query (for IE8) and creates a slightly modified grid for IE7 and below. Both receive a fixed-width 960px wide container as these browsers will be used on desktop machines.

## What’s included

Examples of 10 different grid configurations:

- **Basic** : create a normal 2-column grid at any breakpoint
- **Changing** : create a grid that changes from 1-column, to 2-column and then to 1/3rd and 2/3rds
- **Jumping** : three columns where one jumps alongside the other at breakpoint 2
- **Nested** : example of grids which can easily be nested!
- **Smaller gutter** : adding the `.half-gutter` class to `.grid-wrap` to make the gutter half the size (you can change the base gutter value in `proportional-grids.scss`)
- **Blocked** : using the `.island` wrapper to create columns with backgrounds
- **No gutter** : adding the `.no-gutter` class to remove gutters entirely
- **No additional classes** : use a class on `.grid-wrap` e.g. `bp1-col-set-one-quarter` to set *all* columns to that width at a given breakpoint, without the need for classes on each column itself
- **Complex grid system** : a mixture of the above, using the `.reset-gutter` to reset the gutter of a nested grid

All Sass files are provided which makes it far easier to compile your grid by including one mixin per breakpoint and then repeating each one in `ie.scss`. Alternatively, do away with a separate IE stylesheet using the method below.

## Added support

Mixins have been added to work using [Jake Archibald's Sass-IE method](http://goo.gl/uwyT6), meaning grids for IE can be *automatically* created with their media queries stripped out (so no need for a specific `ie.css` stylesheet).

With this in place, in `styles.scss` instead of using:

	/* -- Breakpoint (.bp1)
	------------------------------------------------------------- */			
	@media only screen and (min-width: 30em) {
	    @include grid-setup("bp1-col");
	}

...include your grids using:

	@include respond-min(30em) {
		@include grid-include("bp1-col")
	}

...to include each set of grid classes you wish to use in your HTML.
