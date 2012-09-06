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

Examples of 6 different grid configurations including blocked, nested, and one with smaller gutters (just by adding a single class to `.grid-wrap`). Sass files are provided which makes it far easier to compile your grid by including one mixin per breakpoint and then repeating each one in `ie.scss`.