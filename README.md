# sass-smacss 0.2.7
By <a href="http://twitter.com/leongaban">@leongaban</a>

### Scalable and modular architecture for CSS https://smacss.com | http://sass-lang.com

![Bower, SMACSS, SASS](https://raw.githubusercontent.com/leongaban/github_images/master/bower-jack-sass.png)

##### SMACSS is a style guide for writing and organizing SASS modules.

##### Steps to install
Install <a href="https://nodejs.org/">Node</a> (which comes with <a href="https://www.npmjs.com/">NPM</a>): https://nodejs.org/

Install <a href="http://bower.io">Bower</a>: `npm install -g bower`

Finally install sass-smacss with Bower: `$ bower install sass-smacss`

Main sass module: `bower_components > sass-smacss > sass > main.scss`

<strong>The layout tree below, the module layouts imports all sectional styles from the layouts folder:</strong>

```
/*==========================================================
Master Stylesheet
============================================================

stylesheets/
|-- vendors/
|   |-- _reset # Eric Meyer's reset v2.0.0
|
|-- modules/
|   |-- _base # Imports all the modules
|   	|-- _animation
|   	|-- _colors
|   	|-- _fonts
|   	|-- _mixins
|
|   |-- _defaults
|   |-- _buttons
|   |-- _fonts
|   |-- _inputs
|   |-- _layout
|   	|-- header
|   	|-- home
|   	|-- footer
|   	...
|
|   |-- _svg
|   |-- _queries
|
|-- vendors/
|   |-- _normalize # Nicolas Gallagher v3.0.2
|   ...
|
`-- main
*/

@import "vendors/normalize";
@import "vendors/reset";
@import "modules/base";
@import "modules/defaults";
@import "modules/inputs";
@import "modules/buttons";
@import "modules/components";
@import "modules/svg";
@import "modules/queries";
```

<strong>Next are the normalize and reset modules. Base module imports the mixins, colors and other less frequently updated settings/modules:</strong>

```
@import "mixins";
@import "colors";
@import "fonts";
@import "animation";
```

<strong>Colors</strong>
```
// Primary
$blue: 			#024562;
$green: 		#249B7A;
$orange: 		#FC913A;
$red: 			#F25A43;
$gray:			#454545;

// Brands
$facebook: 	#438acb;
$twitter: 	#5cbde9;

// Elements
$body: 			#fff;
$button: 		$blue;
$buttonHover:	lighten($blue, 10%);
```

<strong>Defaults.scss is where all main non-custom elements are set:</strong>

```
/* Start of styles | Defaults
==================================================== */
html, body { width: 100%; height: 100%; }

body {
	overflow-x: hidden;
  // font-family: 'Ubuntu', sans-serif; // <- choose your body font
	// font-weight: 300;
  font-size: em(16);
  color: #666;
	background: $body;
}

...
```

<strong>Then modules such as inputs, tables, buttons etc should follow:</strong>
```
@import "modules/inputs";	// Inputs & Selects
@import "modules/buttons";	// Buttons
```

<strong>Next comes the layout module which starts importing your layouts:</strong>
```
/* Layouts
==================================================== */

// Header
@import "../layouts/header";

// Add whatever views you want here...

// Footer
@import "../layouts/footer";
```

<strong>Finally the SVG or PNG and <i>media queries</i> modules.</strong>
```
@import "modules/svg";
@import "modules/queries";
```

<strong>In the SVG module it's recommended to just add class names here, then in the modules where those classes are used, set the visual properties.</strong>

```
// Profile | profile.scss
.green-phone-icon,
.remove-info,
.dropdown-arrow,

// Reports | reports.scss
.check-green,
.check-red,
.css-label,

// Errors | alerts.scss
.lost-man {
  background-size: 1600px 1600px;
  background-image: url(/static/img/dashboard/icons.svg), none;
}
```

<strong>Class in seperate module using the SVG background image.</strong>
```
.green-phone-icon {
  float: left;
  width: 24px;
  height: 24px;
  margin: 5px 10px;
  background-position: -50px -150px;
}
```

<strong>Added custom mixin function for creating multiple colored items</strong>
```
/*
    Custom mixin | colored-tag
    usage:

    .tag {
        border: 1px solid $gray_light;
        background: $gray_bg;
        @include transition(all, .2s, ease-out);

        &.blue1 { @include colored-tag($blue1) }
        &.blue2 { @include colored-tag($blue2) }
        &.blue3 { @include colored-tag($blue3) }
    }

 */

@mixin colored-tag($kolor) {
    border: 1px solid $kolor;
    background: $kolor;

    @if $kolor == $yellow {
        color: $gray4;
        &:hover {
            border: 1px solid $kolor !important;
            background: lighten($kolor, 20%) !important;
        }
    } @else if $kolor == $gold {
        color: $gray4;
        &:hover {
            border: 1px solid $kolor !important;
            background: lighten($kolor, 20%) !important;
        }
    } @else if $kolor == $orange {
        color: $gray4;
        &:hover {
            border: 1px solid $kolor !important;
            background: lighten($kolor, 20%) !important;
        }
    } @else {
        color: #fff;
        &:hover {
            // color: $gray4;
            border: 1px solid $kolor !important;
            background: lighten($kolor, 10%) !important;
        }
    }
}
```
