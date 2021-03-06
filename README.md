[![npm][npm]][npm-url]
[![deps][deps]][deps-url]
[![test][test]][test-url]
[![coverage][cover]][cover-url]
[![quality][quality]][quality-url]
[![chat][chat]][chat-url]

<div align="center">
  <!-- replace with accurate logo e.g from https://worldvectorlogo.com/ -->
  <a href="https://github.com/webpack/webpack">
    <img width="200" height="200" vspace="" hspace="25"
      src="https://cdn.rawgit.com/webpack/media/e7485eb2/logo/icon.svg">
  </a>
  <h1>Babili Webpack Plugin</h1>
  <p>A Webpack Plugin for <a href="https://github.com/babel/babili">Babili</a> - A babel based minifier<p>
</div>

<h2 align="center">Install</h2>

```bash
npm install babili-webpack-plugin --save-dev
```

<h2 align="center">Usage</h2>

```js
// webpack.config.js
const BabiliPlugin = require("babili-webpack-plugin");
module.exports = {
  entry: //...,
  output: //...,
  plugins: [
    new BabiliPlugin(babiliOptions, overrides)
  ]
}
```

<h2 align="center">Options</h2>

#### babiliOptions

`babiliOptions` are passed on to the babili preset. You can find a list of [all available options](https://github.com/babel/minify/tree/master/packages/babel-preset-minify#options) in the package directory. 

`Default: {}`

#### Overrides

+ `test`: JS file extension regex. Default: `/\.js($|\?)/i`
+ `comments`: Preserve Comments. Default: `/@preserve|@licen(s|c)e/`. falsy value to remove all comments. Accepts function, object with property test (regex), and values.
+ `sourceMap`: Default: uses [webpackConfig.devtool](https://webpack.js.org/configuration/devtool/). Set this to override that.
+ `parserOpts`: Configure babel with special parser options.
+ `babel`: Pass in a custom babel-core instead. `require("babel-core")`
+ `babili`: Pass in a custom babili preset instead - `require("babel-preset-babili")`.
``

<h2 align="center">Why</h2>

You can also use [babel-loader](https://github.com/babel/babel-loader) for webpack and include `babili` [as a preset](https://github.com/babel/babili#babel-preset) and should be much faster than using this - as babili will operate on smaller file sizes. But then, why does this plugin exist at all? -

+ A webpack loader operates on single files and babili preset as a webpack loader is going to consider each file to be executed directly in the browser global scope (by default) and will not optimize some things in the toplevel scope. This is going to change and you can opt-in to optimize toplevel scope - [babel/babili#210](https://github.com/babel/babili/issues/210), [babel/babili#203](https://github.com/babel/babili/issues/203), etc...
+ When you exclude `node_modules` from being run through the babel-loader, babili optimizations are not applied to the excluded files as it doesn't pass through the minifier.
+ When you use the babel-loader with webpack, the code generated by webpack for the module system doesn't go through the loader and is not optimized by babili.
+ A webpack plugin can operate on the entire chunk/bundle output and can optimize the whole bundle and you can see some differences in minified output. But this will be a lot slower as the file size is usually really huge. So there is [another idea](https://github.com/boopathi/babili-webpack-plugin/issues/8) where we can apply some optimizations as a part of the loader and some optimizations in a plugin.

<h2 align="center">Maintainers</h2>

<table>
  <tbody>
    <tr>
      <td align="center">
        <img width="150" height="150"
        src="https://avatars2.githubusercontent.com/u/294474?v=3&s=150">
        </br>
        <a href="https://github.com/boopathi">Boopathi Rajaa</a>
      </td>
      <td align="center">
        <img width="150" height="150"
        src="https://avatars3.githubusercontent.com/u/166921?v=3&s=150">
        </br>
        <a href="https://github.com/bebraw">Juho Vepsäläinen</a>
      </td>
      <td align="center">
        <img width="150" height="150"
        src="https://avatars2.githubusercontent.com/u/8420490?v=3&s=150">
        </br>
        <a href="https://github.com/d3viant0ne">Joshua Wiens</a>
      </td>
      <td align="center">
        <img width="150" height="150"
        src="https://avatars3.githubusercontent.com/u/533616?v=3&s=150">
        </br>
        <a href="https://github.com/SpaceK33z">Kees Kluskens</a>
      </td>
      <td align="center">
        <img width="150" height="150"
        src="https://avatars3.githubusercontent.com/u/3408176?v=3&s=150">
        </br>
        <a href="https://github.com/TheLarkInn">Sean Larkin</a>
      </td>
    </tr>
  <tbody>
</table>

[npm]: https://img.shields.io/npm/v/babili-webpack-plugin.svg
[npm-url]: https://npmjs.com/package/babili-webpack-plugin

[deps]: https://david-dm.org/webpack-contrib/babili-webpack-plugin.svg
[deps-url]: https://david-dm.org/webpack-contrib/babili-webpack-plugin

[chat]: https://img.shields.io/badge/gitter-webpack%2Fwebpack-brightgreen.svg
[chat-url]: https://gitter.im/webpack/webpack

[test]: https://travis-ci.org/webpack-contrib/babili-webpack-plugin.svg?branch=master
[test-url]: https://travis-ci.org/webpack-contrib/babili-webpack-plugin

[cover]: https://codecov.io/gh/webpack-contrib/babili-webpack-plugin/branch/master/graph/badge.svg
[cover-url]: https://codecov.io/gh/webpack-contrib/babili-webpack-plugin

[quality]: https://www.bithound.io/github/webpack-contrib/babili-webpack-plugin/badges/score.svg
[quality-url]: https://www.bithound.io/github/webpack-contrib/babili-webpack-plugin
