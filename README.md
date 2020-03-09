# Sparticles
**Lightweight, _High Performance_ Particles in Canvas.**  
Designed for those occasions when you ***✨ just ✨ have ✨ to ✨ have ✨*** sparkles, 
snow, or stars on your fantastic homepage!

![Image of little coloured stars known as "Sparticles" running at 120fps](example/example.png)

# installation

Depending on how your project looks, 
- you may want to [include a direct link to the script](#vanilla) and 
then initialise the sparkles,
- or you may want
to [import the module in to your application](#bundler) for a more modern approach.

## vanilla

1. firstly make sure you've downloaded [the latest version of the script](https://github.com/simeydotme/sparticles/releases) 
to your application directory _(if you are running on a CMS you might also 
need to upload the file to your server)_. The file you'll want to use is; `dist/sparticles.min.js` 
to make sure it downloads the fastest for your users.

2. After you've downloaded, or uploaded, the `sparticles.min.js` file to the 
correct place, you'll then need to include it in your web page;

```html
<script src="../path/to/sparticles.min.js"></script>
```

3. And finally, you should then be able to initialise the sparticles by 
running this code in your javascript; <sup>_(make sure this code runs _after_ 
you've included the script above.)_</sup>

```html
<script>
  window.onload = function() {
    var myElement = document.getElementById("myDiv");
    var mySparticles = new Sparticles(myElement, { speed: 10 }, 400);
  }
</script>
```

## jquery

For jQuery sites, you may follow all of the steps above, but replace 
the third step with something like below;

```html
<script>
  var $el = $("#myDiv");
  var mySparticles = new Sparticles($el[0], { speed: 10 }, 400);
</script>
```

## app / bundler

If you're running a more modern type of application with something like Svelte or VueJs; 

1. First you will want to install the module with NPM;

```bash
yarn add sparticles
# or npm, if you prefer
```

2. Then import the module in to the app where you want to use it

```js
import Sparticles from "sparticles";
```

3. Finally initialise with vanillaJS

```js
new Sparticles(node, { speed: 10 }, 400);
```

4. If you're using SvelteJS specifically, then your single-file component
would look a little like this;

```html
<script>

  import Sparticles from "sparticles";

  let sparticles,
      options = { color: "gold", shape: "star", speed: 50 };

  function addSparticles(node) {
    new Sparticles(node, options, 400);
  }

</script>

<main use:addSparticles>
</main>
```

# usage

Providing that the script/module has been properly included, then it can be initialised
by running the `Sparticles()` constructor;
```js
var mySparticles = new Sparticles();
```

# parameters

When initialising the Sparticles instance there are some parameters that can be supplied.

parameter                   | type               | default            | description
----------------------------|--------------------|--------------------|-----------------------------------------------------------
**node**                    | `HTMLElement`      | `document.body`    | the element in the DOM which the Sparticles will append to
**[options](#options)**     | `Object`           | `{}`               | an object with [all the options for the instance](#options)
**width**                   | `Number`           | `node.clientWidth` | the width of the canvas element
**height**                  | `Number`           | `node.clientWidth` | the height of the canvas element (defaults to width)

<sup>Leave the `width`/`height` properties empty to make the canvas resize to fit it's `node`</sup>

---

- Supply nothing and get a default Sparticle instance on the `<body>`
```js
var mySparticles = new Sparticles();
```

- Supply a single HTMLElement parameter for a default Sparticle instance on that element
```js
var mySparticles = new Sparticles(document.getElementById("myDiv"));
```

- Supply a single `Object` parameter to customise a Sparticle instance on the `<body>`
```js
var mySparticles = new Sparticles({ color: "red" });
```

- Supply the width and height parameters for a custom size
```js
var mySparticles = new Sparticles({ color: "red" }, 400, 300);
```

# options

A brief look at all the options, with more details below.

option                              | type              | default         | description
------------------------------------|-------------------|-----------------|-----------------------------------------------------
**[composition](#composition)**     | `String`          | `source-over`   | canvas globalCompositeOperation value for particles
**[count](#count)**                 | `Number`          | `50`            | number of particles on the canvas simultaneously
**[speed](#speed)**                 | `Number`          | `10`            | default velocity of every particle
**[parallax](#parallax)**           | `Number`          | `1`             | speed multiplier effect for larger particles (0 = none)
**[direction](#direction)**         | `Number`          | `180`           | default direction of particles in degrees (0 = ↑, 180 = ↓)
**[xVariance](#xVariance)**         | `Number`          | `2`             | random deviation of particles on x-axis from default direction
**[yVariance](#yVariance)**         | `Number`          | `2`             | random deviation of particles on y-axis from default direction
**[rotate](#rotate)**               | `Boolean`         | `true`          | can particles rotate
**[rotation](#rotation)**           | `Number`          | `1`             | default rotational speed for every particle
**[alphaSpeed](#alphaSpeed)**       | `Number`          | `10`            | rate of change in alpha over time
**[alphaVariance](#alphaVariance)** | `Number`          | `1`             | random deviation of alpha change
**[minAlpha](#minAlpha)**           | `Number`          | `0`             | minumum alpha value of every particle
**[maxAlpha](#maxAlpha)**           | `Number`          | `1`             | maximum alpha value of every particle
**[minSize](#minSize)**             | `Number`          | `1`             | minimum size of every particle
**[maxSize](#maxSize)**             | `Number`          | `10`            | maximum size of every particle
**[style](#style)**                 | `String`          | `fill`          | fill style of particles (one of; "fill", "stroke" or "both")
**[bounce](#bounce)**               | `Boolean`         | `false`         | should the particles bounce off edge of canvas
**[drift](#drift)**                 | `Number`          | `1`             | the "driftiness" of particles which have a horizontal/vertical direction
**[glow](#glow)**                   | `Number`          | `0`             | the glow effect size of each particle
**[twinkle](#twinkle)**             | `Boolean`         | `false`         | particles to exhibit an alternative alpha transition as "twinkling"
**[color](#color)**                 | `String`/`Array`  | `rainbow`       | css color as string, or array of color strings (can also be "rainbow")
**[rainbowColor](#rainbowColor)**   | `Function`        | `randomHsl`     | function for returning a random/rainbow color when the color is set as "rainbow"
**[shape](#shape)**                 | `String`/`Array`  | `circle`        | shape of particles (any of; circle, square, triangle, diamond, line, image) or "random"
**[imageUrl](#imageUrl)**           | `String`/`Array`  |                 | if shape is "image", define an image url (can be data-uri, should be square (1:1 ratio))

---

## `composition`
- Type: `String` 
- Default: `source-over`
- Possible: [`see list here`](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/globalCompositeOperation)

The [global render composition](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/globalCompositeOperation)
when rendering particles on top of one-another. This, however, is a very expensive operation when set to anything
other than the default value (`source-over`), and will ultimately degrade performance, especially with many particles.

Will accept [any of the values that are provided as part of the Canvas API](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/globalCompositeOperation)

## `count`
- Type: `Number`
- Default: `50`
- Range: `1 - 10000`

Simply the number of particles drawn to the screen.  
Values over `500` may begin to degrade performance.

## `speed`
- Type: `Number`
- Default: `10`
- Range: `0 - 100`

The base value of speed across all particles. This is modified by options such as 
`parallax` and `[x/y]Variance` to determine the final velocity of each individual particle.
A speed of `0` will render particles stationary before applying `[x/y]Variance`.

## `parallax`
- Type: `Number`
- Default: `1`
- Range: `0 - 20`

A value to apply more speed to larger particles, and less speed to smaller particles, creating
an effect which makes larger particles appear closer to the screen.

## `direction`
- Type: `Number`
- Default: `180`
- Range: `0 - 360`

The base angle (in degrees) at which the particles are travelling, so long as they have a speed value.

## `xVariance`
- Type: `Number`
- Default: `2`
- Range: `0 - 20`

How much variance is applied between particles on the `X` axis. A value of `0` will make all particles
appear to be going completely parallel, and look unnatural.

Can be used in conjunction with `speed: 0;` to make particles which float randomly in space.

## `yVariance`
- Type: `Number`
- Default: `2`
- Range: `0 - 20`

How much variance is applied between particles on the `Y` axis. A value of `0` will make all particles
appear to be going completely parallel, and look unnatural.

Can be used in conjunction with `speed: 0;` to make particles which float randomly in space.

## `rotate`
- Type: `Boolean`
- Default: `true`

Toggle whether the particles are allowed to spin about their axis.

## `rotation`
- Type: `Number`
- Default: `1`
- Range: `0 - 20`

How fast the particles can spin about their axis, this has a random multiplier added per-particle
which prevents a completely unnatural spinning effect.

## `alphaSpeed`
- Type: `Number`
- Default: `10`
- Range: `0 - 50`

Rate of change for the alpha value of all particles. A higher value will encourage the particles
to flicker like candle lights. A value of `0` will disable alpha change.

## `alphaVariance`
- Type: `Number`
- Default: `2`
- Range: `0 - 10`

How much variance is applied between each particle on the alpha value change over time. A value
of `0` will cause all particles to change alpha at the same rate, a higher value will introduce more
variety.

## `minAlpha`
- Type: `Number`
- Default: `0`
- Range: `-5 - +1`

The minimum alpha value a particle can change to. The lower the number the longer it will stay invisible
on the canvas, this could be useful in some scenarios where the particle should fade out for a while.

Must be lower than the `maxAlpha` value.

## `maxAlpha`
- Type: `Number`
- Default: `0`
- Range: `0 - +5`

The maximum alpha value a particle can change to. The higher the number the longer it will stay visible
on the canvas, this could be useful in some scenarios where the particle should stay at max alpha for a time.

Must be higher than the `minAlpha` value.

## `minSize`
- Type: `Number`
- Default: `1`
- Range: `1 - 100`

Minimum size (in pixels) of the particles. The actual size of each particle is variable between the `minSize`
and `maxSize`. If the `minSize` and `maxSize` are the same value; then all particles will be uniformly sized.

## `maxSize`
- Type: `Number`
- Default: `10`
- Range: `1 - 100`

Maximum size (in pixels) of the particles. The actual size of each particle is variable between the `minSize`
and `maxSize`. If the `minSize` and `maxSize` are the same value; then all particles will be uniformly sized.

## `style`
- Type: `String`
- Default: `"fill"`
- Values: `"fill"`, `"stroke"` or `"both"`

Particles can be either stroked (outline) or filled (solid) and this setting determines that style. It's
also possible to randomize the style by choosing `"both"`

## `bounce`
- Type: `Boolean`
- Default: `false`

Determine if particles should bounce off the boundaries of the canvas instead of resetting to the opposite side.
This is best used with `speed: 0;` and a high value for `[x/yVariance]` to create a chaotic effect.

## `drift`
- Type: `Number`
- Default: `1`
- Range: `1 - 20`

How much a particle will "drift" as it falls. This is to imply a floatiness/wind effect like seen with snow flakes,
or leaves. The `drift` will only apply if `speed > 0` and `direction` is near to a 90degree value (`0, 90, 180, 270`)

## `glow`
- Type: `Number`
- Default: `0`
- Range: `0 - 50`

Glow (or shadow) effect around the particle. This will not affect images.

## `twinkle`
- Type: `Boolean`
- Default: `false`

Apply a "twinkle" effect to the particle when changing alpha. This works best with a higher `alphaSpeed` and 
`alphaVariance` value.

## `color`
- Type: `String` / `Array<String>`
- Default: `"rainbow"`
- Values: any valid css/html color string

A CSS/HTML color string to apply across all particles.  
If an array of colors (`[ "#ff0", "red", "hsl(10,50%,50%)" ]`) is given, then each particle will 
be assigned a random color from the array. Additionally `"rainbow"` can be used to assign any random color.

## `rainbowColor`
- Type: `Function`
- Default: [`randomHSL()`](https://github.com/simeydotme/sparticles/blob/9a132505c19268a70ec31766119d29cb9bddd0b2/src/helpers.js#L55-L64)
- Arguments: `index`, `total`

Custom function to use when generating "`rainbow`" colors. The default function will return a fairly
pleasant `hsl()` color with a high saturation and medium lightness. This can be overridden to suit
your environment better. The two arguments (`index`, `total`) are `Integer`s and allow for a little
psuedo-randomizing.

**example:**

```js
rainbowColor: function( index, total ) {
	return `hsl( ${index}, 80%, ${total - index}% )`;
}
```

## `shape`
- Type: `String` / `Array<String>`
- Default: `"circle"`
- Values: `"circle"`, `"square"`, `"triangle"`, `"line"`, `"diamond"`, `"star"` or `"image"`

Determine the shape of all the particles.  
If an array of shapes (`[ "circle", "star", "diamond" ]`) is given, then each particle will
be assigned a random shape form the array. Additionally `"image"` can be used to [define a custom
particle shape from an image when combined with `imageUrl`](#imageUrl).

## `imageUrl`
- Type: `String` / `Array<String>`
- Default: `""`
- Values: a valid url, or data-uri

Determine the custom image to be used for all the particles.
If an array of urls (`[ "http://my.image/shape.png", "http://my.svg/shape.svg" ]`) is given, then each particle
will be assigned a random image as it's shape from the array.

This only applies [if the `shape` is set to `"image"`](#shape).


# methods

method                                                   | description
---------------------------------------------------------|------------------------------------------------------
**[destroy()](#destroy)**                                | destroy the Sparticles instance and remove event listeners
**[setCanvasSize( width, height )](#setCanvasSize)**     | set the new size of the canvas
**[resetSparticles()](#resetSparticles)**                | reset all the particles on the canvas


# styling
