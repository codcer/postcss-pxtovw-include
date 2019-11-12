# postcss-pxtovw-include

此工具可以针对性转换特定目录，用法和官方一样，只是加入了 include 这个属性

## Demo

If your project involves a fixed width, this script will help to convert pixels into viewport units.

### Input

```css
.class {
  margin: -10px 0.5vh;
  padding: 5vmin 9.5px 1px;
  border: 3px solid black;
  border-bottom-width: 1px;
  font-size: 14px;
  line-height: 20px;
}

.class2 {
  border: 1px solid black;
  margin-bottom: 1px;
  font-size: 20px;
  line-height: 30px;
}

@media (min-width: 750px) {
  .class3 {
    font-size: 16px;
    line-height: 22px;
  }
}
```

### Output

```css
.class {
  margin: -3.125vw 0.5vh;
  padding: 5vmin 2.96875vw 1px;
  border: 0.9375vw solid black;
  border-bottom-width: 1px;
  font-size: 4.375vw;
  line-height: 6.25vw;
}

.class2 {
  border: 1px solid black;
  margin-bottom: 1px;
  font-size: 6.25vw;
  line-height: 9.375vw;
}

@media (min-width: 750px) {
  .class3 {
    font-size: 16px;
    line-height: 22px;
  }
}
```

## Getting Started

### Installation

Add via npm

```
$ npm install postcss-px-to-viewport --save-dev
```

or yarn

```
$ yarn add -D postcss-px-to-viewport
```

### Usage

Default Options:

```js
{
  unitToConvert: 'px',
  viewportWidth: 320,
  unitPrecision: 5,
  propList: ['*'],
  viewportUnit: 'vw',
  fontViewportUnit: 'vw',
  selectorBlackList: [],
  minPixelValue: 1,
  mediaQuery: false,
  replace: true,
  exclude: [],
  landscape: false,
  landscapeUnit: 'vw',
  landscapeWidth: 568
}
```

- `unitToConvert` (String) unit to convert, by default, it is px.
- `viewportWidth` (Number) The width of the viewport.
- `unitPrecision` (Number) The decimal numbers to allow the vw units to grow to.
- `propList` (Array) The properties that can change from px to vw.
  - Values need to be exact matches.
  - Use wildcard _ to enable all properties. Example: ['_']
  - Use * at the start or end of a word. (['*position\*'] will match background-position-y)
  - Use ! to not match a property. Example: ['*', '!letter-spacing']
  - Combine the "not" prefix with the other prefixes. Example: ['*', '!font*']
- `viewportUnit` (String) Expected units.
- `fontViewportUnit` (String) Expected units for font.
- `selectorBlackList` (Array) The selectors to ignore and leave as px.
  - If value is string, it checks to see if selector contains the string.
    - `['body']` will match `.body-class`
  - If value is regexp, it checks to see if the selector matches the regexp.
    - `[/^body$/]` will match `body` but not `.body`
- `minPixelValue` (Number) Set the minimum pixel value to replace.
- `mediaQuery` (Boolean) Allow px to be converted in media queries.
- `replace` (Boolean) replaces rules containing vw instead of adding fallbacks.
- `exclude` (Array or Regexp) Ignore some files like 'node_modules'
  - If value is regexp, will ignore the matches files.
  - If value is array, the elements of the array are regexp.
- `landscape` (Boolean) Adds `@media (orientation: landscape)` with values converted via `landscapeWidth`.
- `landscapeUnit` (String) Expected unit for `landscape` option
- `landscapeWidth` (Number) Viewport width for landscape orientation.

#### Use with gulp-postcss

add to your `gulpfile.js`:

```js
var gulp = require("gulp");
var postcss = require("gulp-postcss");
var pxtoviewport = require("postcss-px-to-viewport");

gulp.task("css", function() {
  var processors = [
    pxtoviewport({
      viewportWidth: 320,
      viewportUnit: "vmin"
    })
  ];

  return gulp
    .src(["build/css/**/*.css"])
    .pipe(postcss(processors))
    .pipe(gulp.dest("build/css"));
});
```

#### Use with PostCss configuration file

add to your `postcss.config.js`

```js
module.exports = {
  plugins: {
    ...
    'postcss-px-to-viewport': {
      // options
    }
  }
}
```

## Running the tests

In order to run tests, you need to install `jasmine-node` globally:

```
$ npm install jasmine-node -g
```

Then run the tests via npm script:

```
$ npm run test
```

## Contributing

Please read [Code of Conduct](CODE-OF-CONDUCT.md) and [Contributing Guidelines](CONTRIBUTING.md) for submitting pull requests to us.

## License

This project is licensed under the [MIT License](LICENSE).

## Acknowledgments

- Hat tip to https://github.com/cuth/postcss-px-to-viewport/ for inspiring us for this project.
