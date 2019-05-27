# SASS

```scss
/* Block comments */
// Line comments

@import './other_sass_file`;

Mixin
@mixin font-size($n) {
  font-size: $n * 1.2em;
}
body {
  @include font-size(2);
}

@mixin heading-font {
  font-family: sans-serif;
  font-weight: bold;
}
h1 {
  @include heading-font;
}
Media
$desktop:720px;
@mixin desktop{
	@media (min-width: #{$desktop}){
		@content;
	}
}
span{
	@include desktop{
		//style
	}
}

Var & Nesting
$red: #833;
.markdown-body {
&:hover {  // > .markdown-body:hover
    color: $red;
  }
}

Extend
.button {
  ···
}
.push-button {
  @extend .button;
}

Maps
$map: (key1: value1, key2: value2, key3: value3);
map-get($map, key1)

/* From <https://devhints.io/sass> */
```

## Color

```scss
rgb(100, 120, 140)
rgba(100, 120, 140, .5)
rgba($color, .5)

mix($a, $b, 10%)   // 10% a, 90% b
darken($color, 5%)
lighten($color, 5%)
saturate($color, 5%)
desaturate($color, 5%)
grayscale($color)
adjust-hue($color, 15deg)
compliment($color)    // like adjust-hue(_, 180deg)
invert($color)
fade-in($color, .5)   // aka opacify()
fade-out($color, .5)  // aka transparentize() - halves the opacity
rgba($color, .5)      // sets alpha to .5

// Changes by fixed amounts
adjust-color($color, $blue: 5)
adjust-color($color, $lightness: -30%)   // like darken(_, 30%)
adjust-color($color, $alpha: -0.4)       // like fade-out(_, .4)
adjust-color($color, $hue: 30deg)        // like adjust-hue(_, 15deg)
// Changes via percentage
scale-color($color, $lightness: 50%)
// Changes one property completely
change-color($color, $hue: 180deg)
change-color($color, $blue: 250)
```

## Functions

```scss
Strings
unquote('hello')
quote(hello)
to-upper-case(hello)
to-lower-case(hello)
str-length(hello world)
str-slice(hello, 2, 5)      // "ello" - it's 1-based, not 0-based
str-insert("abcd", "X", 1)  // "Xabcd"

Numbers
floor(3.5)
ceil(3.5)
round(3.5)
abs(3.5)
min(1, 2, 3)
max(1, 2, 3)
percentage(.5)   // 50%
random(3)        // 0..3
```

## If-Loop

```scss
@if $position == 'left' {
   position: absolute;
   left: 0;
}
@else {
   position: static;
}

// Loop
@for $i from 1 through 4 {
  .item-#{$i} { left: 20px * $i; }
}

// While loops
$i: 6;
@while $i > 0 {
  .item-#{$i} { width: 2em * $i; }
  $i: $i - 2;
}

// Each loops (simple)
$menu-items: home about services contact;
@each $item in $menu-items {
  .photo-#{$item} {
    background: url('images/#{$item}.jpg');
  }
}

// Each loops (nested)
$backgrounds: (home, 'home.jpg'), (about, 'about.jpg');
@each $id, $image in $backgrounds {
  .photo-#{$id} {
    background: url($image);
  }
}
```

## Interpolation

```scss
.#{$klass} { ... }      // Class
call($function-name)    // Functions
@media #{$tablet}
font: #{$size}/#{$line-height}
url("#{$background}.jpg")
```

## Lists

```scss
$list: (a b c);
nth($list, 1)  // starts with 1
length($list)
@each $item in $list { ... }
```