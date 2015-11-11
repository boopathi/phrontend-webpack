# yawc

[![Build Status](https://travis-ci.org/flipkart-incubator/phrontend-webpack.svg?branch=master)](https://travis-ci.org/flipkart-incubator/phrontend-webpack) [![Code Climate](https://codeclimate.com/github/flipkart-incubator/phrontend-webpack/badges/gpa.svg)](https://codeclimate.com/github/flipkart-incubator/phrontend-webpack) [![Test Coverage](https://codeclimate.com/github/flipkart-incubator/phrontend-webpack/badges/coverage.svg)](https://codeclimate.com/github/flipkart-incubator/phrontend-webpack/coverage) [![npm version](https://badge.fury.io/js/phrontend-webpack.svg)](http://badge.fury.io/js/phrontend-webpack)

Yet Another Webpack Config maker. 

## Install

```sh
npm install yawc --save
```

in your phrontend application.

## Options

##### `src : String<Path>`

+ The source directory for app. Usually it is `__dirname/app` or `__dirname`.
+ Must be an absolute path

##### `dest : String<Path>`

+ The destination/output directory
+ If relative, it is considered to be relative to `src`

##### `library : String<Name>`

+ Your exports from your entry will be available under this global
+ `window.<library> = <exports>`

##### `publicPath : String`

+ default: `public/`
+ make sure this matches dest
+ usually used to specify CDN base URL for prod

##### `minimize : Boolean`

+ cache busting + minification
+ `true` - minified JS, JS filenames contain hashes, css classnames are just hashes
+ `false` - long classnames for css - path, filename, classname, hash, JS filenames don't contain hashes

##### `hot : Boolean`

+ Enables react-hot-loader for modules
+ This is disabled for css when separateStyleSheet is enabled

##### `separateStylesheet : Boolean`

+ If true, it outputs a separate css file using extract-text-webpack-plugin
+ Uses inline stylesheets otherwise

##### `transpile : String<PackageName> | Array<PackageName>`

+ Transpile these packages present in node_modules directory

##### `cssLocalImports : Boolean`

+ By default(true) css can be imported into JS only from the current directory
+ If false, you can do `import styles from '../../styles.css'`;

##### `moduleDirectories : String<Path> | Array<Path>`

+ Absolute paths are inserted as it is to resolve.root of webpack
+ If relative, it'll be considered relative to `src`

##### `dedupe : Boolean`

+ Use webpack dedupe plugin

##### `debug : Boolean`

+ Switch loaders to debug mode.

##### `devtool : String`

+ default: `cheap-module-inline-source-map`

##### `browsers`

+ options passed to autoprefixer's `.browsers`

## Example

```js
var path = require('path');
var makeConfig = require('yawc');
var __PROD__ = process.env.NODE_ENV==='production';
var __DEV__  = !__PROD__;

module.exports = makeConfig({
  src: __dirname, // required
  dest: './dist',
  library: 'todoapp',
  publicPath: __DEV__ ? 'dist/' : 'https://cdn.server/path/to/bundleDir',
  minimize: __PROD__,
  hot: __DEV__,
  separateStylesheet: __PROD__,
  transpile: 'my-other-module',
  cssLocalImports: true,
  moduleDirectories: path.join(__dirname, 'components'),
  dedupe: __PROD__,
  debug: __DEV__,
  devtool: __PROD__ ? 'source-map' : 'cheap-module-inline-source-map',
  browsers: ['Chrome > 36']
});
```
