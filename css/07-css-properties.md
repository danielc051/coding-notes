## CSS3 Properties

**border-radius**

```css
-webkit-border-radius: 4px;
-moz-border-radius: 4px;
border-radius: 4px;
```

Allows rounded corners in elements. Can also be used to create circles.

*Support: IE9+*

**box-shadow**

```css
-webkit-box-shadow: 1px 1px 3px #292929;
-moz-box-shadow: 1px 1px 3px #292929;
box-shadow: 1px 1px 3px #292929;
```

The box-shadow property allows us to easily implement multiple drop shadows (outer or inner) on box elements, specifying values for color, size, blur and offset.

box-shadow accepts four parameters: x-offset, y-offset, blur, color of shadow.

* The first value defines the horizontal offset of the shadow, with a positive value offsetting the shadow to the right of the element, and a negative value to the left.
* The second value defines the vertical offset of the shadow, with a positive value offsetting the shadow from the bottom of the element, and a negative value from the top.
* If supplied, an optional third value defines the blur distance of the shadow. Only positive values are allowed, and the larger the value, the more the shadow’s edge is blurred.
* An optional fourth value can be supplied to define the spread distance of the shadow. A positive value will cause the shadow shape to expand in all directions, while a negative value will cause the shadow shape to contract.

An optional ‘inset’ keyword can be supplied, preceding the length and color values. If present, this keyword causes the shadow to be drawn inside the element.

```css
-webkit-box-shadow: 0 0 20px #333 inset;
-moz-box-shadow: 0 0 20px #333 inset;
box-shadow: 0 0 20px #333 inset;
```

text-shadow has the same set of properties as well.

It allows you to immediately apply depth to your elements. We can apply multiple shadows by using comma as a separator.

*Support: IE9+*

*More reading:*

[Box-shadow, one of CSS3’s best new features](http://www.css3.info/preview/box-shadow/)

[CSS Almanac: box-shadow](https://css-tricks.com/almanac/properties/b/box-shadow/)

**text-shadow**

```css
color: #fff /* text color to white */
text-shadow: 0 0 50px #333;
```

Text shadows are like box shadows except that they are shadows for text rather than the whole element. Luckily, there is no vendor prefix necessary for text shadow.

The options for text shadow are the same as for box-shadow except that there is *no inset* text shadow support.

As with box shadows, it is possible to have multiple text shadows just by separating them with commas. Here is an example that creates a flaming text effect.

```css
text-shadow: 0 0 4px #ccc,
             0 -5px 4px #ff3,
             2px -10px 6px #fd3,
             -2px -15px 11px #f80,
             2px -18px 18px #f20;
```

*Support: IE10+*

**Gradients**

Just as you can declare the background of an element to be a solid color in CSS, you can also declare that background to be a gradient. Using gradients declared in CSS, rather using an actual image file, is better for control and performance.

Gradients are typically one color that fades into another, but in CSS you can control every aspect of how that happens, from the direction to the colors (as many as you want) to where those color changes happen.

```css
.gradient {
  /* can be treated like a fallback */
  background-color: red;

  /* will be "on top", if browser supports it */
  background-image: linear-gradient(red, orange);

  /* these will reset other properties, like background-position, but it does know what you mean */
  background: red;
  background: linear-gradient(red, orange);
}
```

*Support: IE10+*

***Linear Gradient***

Perhaps the most common and useful type of gradient is the linear-gradient(). The gradients "axis" can go from left-to-right, top-to-bottom, or at any angle you chose. Not declaring an angle will assume top-to-bottom.
To make it left-to-right, you pass an additional parameter at the beginning of the linear-gradient() function starting with the word "to", indicating the direction, like "to right". This "to" syntax works for corners as well.
You aren't limited to just two colors either. In fact you can have as many comma-separated colors as you want.
You can also declare where you want any particular color to "start". Those are called "color-stops". Say you wanted yellow to take up the majority of the space, but red only a little bit in the beginning, you could make the yellow color-stop pretty early:

```css
.gradient {
  height: 100px;
  background-image:
    linear-gradient(
      to right,
      red,
      yellow 10%
    );
}
```

***Gotchas***

* We tend to think of gradients as fading colors, but if you have two color stops that are the same, [you can make a solid color instantly change to another solid color](http://codepen.io/chriscoyier/pen/csgoD). This can be useful for declaring a full-height background that simulates columns.

* There are three different syntaxes that browsers have supported:

  - Old: original WebKit-only way, with stuff like from() and color-stop()

  - Tweener: old angle system, e.g. "left"

  - New: new angle system, e.g. "to right"

The way degrees work in the OLD vs NEW syntax is a bit different. The OLD (and TWEENER - usually prefixed) way defines 0deg and left-to-right and proceeds counter-clockwise, while the NEW (usually unprefixed) way defines 0deg as bottom-to-top and proceeds clockwise.

OLD (or TWEENER) = (450 - new) % 360

or even simpler:

NEW = 90 - OLD
OLD = 90 - NEW

like:

OLD linear-gradient(135deg, red, blue)
NEW linear-gradient(315deg, red, blue)

***Radial Gradients***

Radial gradient differ from linear in that they start at a single point and emanate outwards. Gradients are often used to simulate a lighting, which as we know isn't always straight, so they can be useful to make a gradient seem even more natural.

The default is for the first color to start in the (center center) of the element and fade to the end color toward the edge of the element. The fade happens at an equal rate no matter which direction. The default gradient shape is an ellipse.

The possible values for fade  are: closest-corner, closest-side, farthest-corner, farthest-side. You can think of it like: "I want this radial gradient to fade from the center point to the __________, and everywhere else fills in to accommodate that."
A radial gradient doesn't have to start at the default center either, you can specify a certain point by using "at ______" as part of the first parameter.

***Gotchas***

* There are again three different syntaxes that browsers have supported:

  - Old: Prefixed with -webkit-, stuff like from() and color-stop()

  - Tweener: First param was location of center. That will completely break now in browsers that support new syntax unprefixed, so make sure any tweener syntax is prefixed.

  - New: Verbose first param, like "circle closest-corner at top right"

* It is recommended to used autoprefixers like [postcss](https://github.com/postcss/autoprefixer) to handle vendor prefixes to make it work across different browsers consistently.

***Repeating Gradients***

The size of the gradient is determined by the final color stop. If that's at 20px, the size of the gradient (which then repeats) is a 20px by 20px square.

```css
.repeat {
  background-image:
    repeating-linear-gradient(
      45deg,
      yellow,
      yellow 10px,
      red 10px,
      red 20px /* determines size */
    );
}
```

They can be used with both linear and radial varieties.

There is a trick, with non-repeating gradients, to create the gradient in such a way that if it was a little tiny rectangle, it would line up with other little tiny rectangle versions of itself to create a repeating pattern. So essentially create that gradient and set the background-size to make that little tiny rectangle. That made it easy to make stripes, which you could then rotate or whatever.

*More reading:*

[CSS Gradients](https://css-tricks.com/css3-gradients/)

