# CountUp.js
CountUp.js is a dependency-free, lightweight Javascript class that can be used to quickly create animations that display numerical data in a more interesting way.

Despite its name, CountUp can count in either direction, depending on the start and end values that you pass.

CountUp.js supports all browsers. MIT license.


## New in 2.0

- Completely rewritten in **Typescript**! The distributed code is still Javascript.
- **New** cleaner [method signature](#example).
- Tests with **Jest**. As much code coverage as possible mocking requestAnimationFrame.
- **Smart easing**: CountUp intelligently defers easing until it gets close enough to the end value for easing to be visually noticeable. Configureable in the [options](#options).
- **Separate bundles** for with and without the requestAnimationFrame polyfill. Choose `countUp.min.js` for modern browsers or `countUp.withPolyfill.min.js` for IE9 and older, and Opera mini.

CountUp is now distributed as a `commonjs` module - [see below](#including) for how to include it in your project.

## Usage:

**On npm**: `countup.js`

**Params**:
- `target: string | HTMLElement | HTMLInputElement` - id of html element, input, svg text element, or DOM element reference where counting occurs
- `endVal: number` - the value you want to arrive at
- `options?: CountUpOptions` - optional configuration object for fine-grain control

**Options** (defaults in parentheses): <a name="options"></a>

```ts
interface CountUpOptions {
  startVal?: number; // number to start at (0)
  decimalPlaces?: number; // number of decimal places (0)
  duration?: number; // animation duration in seconds (2)
  useGrouping?: boolean; // example: 1,000 vs 1000 (true)
  useEasing?: boolean; // ease animation (true)
  smartEasingThreshold?: number; // smooth easing for large numbers above this if useEasing (999)
  smartEasingAmount?: number; // amount to be eased for numbers above threshold (333)
  separator?: string; // grouping separator (',')
  decimal?: string; // decimal ('.')
  // easingFn: easing function for animation (easeOutExpo)
  easingFn?: (t: number, b: number, c: number, d: number) => number;
  formattingFn?: (n: number) => string; // this function formats result
  prefix?: string; // text prepended to result
  suffix?: string; // text appended to result
  numerals?: string[]; // numeral glyph substitution
}
```

**Example usage**: <a name="example"></a>

```js
const countUp = new CountUp('targetId', 5234);
if (!countUp.error) {
  countUp.start();
} else {
  console.error(countUp.error);
}
```

Pass options:
```js
const countUp = new CountUp('targetId', 5234, options);
```

with optional callback:

```js
countUp.start(someMethodToCallOnComplete);

// or an anonymous function
countUp.start(() => console.log('Complete!'));
```

**Other methods**:

Toggle pause/resume:

```js
countUp.pauseResume();
```

Reset the animation:

```js
countUp.reset();
```

Update the end value and animate:

```js
countUp.update(989);
```

## Including CountUp <a name="including"></a>

CountUp v2 is distributed as a `commonjs` module which means you need to include CountUp in your project using a build tool such as [Webpack](https://webpack.js.org/) or [Browserify](http://browserify.org/).

**Example using Browserify**

Install browserify and countup
```
npm i countup.js
npm i -g browserify
```

main.js:
```js
var countUpModule = require('countup.js');

window.onload = function() {
  var countUp = countUpModule.CountUp('target', 2000);
  countUp.start();
}
```

Build your bundle
```
browserify main.js -o bundle.js
```

Include in your html:
```
<script src="bundle.js"></script>
```
🎉 Done!

## Contributing <a name="contributing"></a>

Before you make a pull request, please be sure to follow these instructions:

1. Do your work on `src/countUp.ts`
1. Run tests: `npm t`
1. Run `npm run build`, which copies and minifies the .js files to the `dist` folder.
1. Test the demo: run `npm run build:demo` then open index.html in a browser and make sure it works.
