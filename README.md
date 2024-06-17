Cardinal spline
===============

A Cardinal spline (basically a Catmull-Rom with a tension option)
implementation for JavaScript which creates an interpolated
smooth curve through each point pair in the given array. There is no
need to specify control points.

![Demo snapshot](https://i.imgur.com/5e69T5C.png)

Additional options are to provide a closed spline as well as segment
resolution (between each point) and of course a tension value.

The archive comes with three separate versions for the sake of convenience:

**curve.js**<br>
Canvas 2D context extension. Call curve() on the context (ctx.curve(...))

**curve_draw.js**<br>
If you prefer not to use an extension then this version provides a clean
function that takes the context as an argument instead.

**curve_calc.js**<br>
Just the internal function that calculates the points. Does not draw
anything.

As well as their minified equivalent. There are no dependencies between
these implementations.


Install
=======

- Git using HTTPS: `git clone https://github.com/epistemex/cardinal-spline-js.git`
- Git using SSH: `git clone git@github.com:epistemex/cardinal-spline-js.git`
- NPM: `npm install /downloads/cardinal-spline-js/` (curve_calc.js / curve_func.js)


Usage
=====

curve.js
--------

Make sure the script is loaded before a 2D context is obtained from the canvas element.

Then use `curve()` as any other method/function on the context -

**Examples**

    ctx.moveTo(points[0], points[1]);  // optionally move to first point
    ctx.curve(points);                 // add cardinal spline to path
    ctx.stroke();                      // stroke path

will draw the points in the array which are arranged in the following manner:

    var points = [x1, y1,  x2, y2, ... xn, yn];

An optional tension value can be given *(default: 0.5)*:

    ctx.curve(points, 0.5);            // sets tension [0.0, 1.0] +/-

a segment resolution value *(default: 25)*:

    ctx.curve(points, 0.5, 25);        // points in each segment

The curve can be drawn closed. All arguments must be given in this
case *(default: false (open))*:

    ctx.curve(points, 0.5, 25, true);  // make a closed loop

The function returns a new (typed) array with the spline points which can be used for
tracking, calculate length and so forth. The values are in floating points:

    var splinePoints = ctx.curve(points);


curve_draw.js
-------------

If you use the function file instead the arguments will be the same as
above except that the context is passed in as the first argument and
then the function is instead called as:

    ctx.moveTo(points[0], points[1]);  // optionally move to first point
    curve(ctx, points);                // add cardinal spline to path
    ctx.stroke();                      // stroke path

Tip: This variant also returns a spline point array.


curve_calc.js
-------------

If you just want to calculate the spline points without drawing anything,
you can use the `curve_calc.js` file and call (please observe that the
name has been changed to better reflect its purpose):

    var splinePoints = getCurvePoints(points, ...);

Context is not required with this function.


In Node.js
----------

Require the package after installing it using npm, then:

    const getCurvePoints = require("cardinal-spline-js").getCurvePoints;
    const outPoints = getCurvePoints(inPoints);

or using ES5 module:

    import { getCurvePoints } from './path/to/curve_calc.js'
    const outPoints = getCurvePoints(inPoints);

Requirements
============

A modern HTML5 compliant browser with support for Typed Arrays and
JavaScript enabled. Except from `curve_calc.js` the canvas element and
a 2D context is required as well.


License
=======

Released under [MIT license](http://choosealicense.com/licenses/mit/).

*&copy; 2013-2018, 2024 Epistemex*

![Epistemex](https://i.imgur.com/wZSsyt8.png)
