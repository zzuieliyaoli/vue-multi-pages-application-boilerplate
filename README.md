# Vue Multi-pages Application Demo

> A Vue multi-pages application demo which is modified by vue-cli

## Steps

After creating projects by `vue init webpack`,
you'd better use these multi-pages application config showing below to replace
all single-page application config.

### Webpack multi-entries

- `build/webpack.base.config.js`

```js
const entries = require('../entries');

module.exports = {
  entry: entries,
  // ...
};
```

### html-webpack-plugin

- `build/webpack.dev.config.js`

```js
const entries = require('../entries');

const htmlPlugins = Object.keys(entries).map(key => (
  new HtmlWebpackPlugin({
    filename: `${key}.html`,
    template: `./src/${key}.html`,
    inject: true,
    chunks: [key],
  })
));

module.exports = {
  // ...
  plugins: [
    // ...
  ].concat(htmlPlugins),
  // ...
};

```

- `build/webpack.prod.config.js`

```js
const entries = require('../entries');

const htmlPlugins = Object.keys(entries).map(key => (
  new HtmlWebpackPlugin({
    filename: path.resolve(__dirname, `../dist/${key}.html`),
    template: `./src/${key}.html`,
    inject: true,
    chunks: ['vendor', 'manifest', key],
    minify: {
      removeComments: true,
      collapseWhitespace: true,
      removeAttributeQuotes: true,
    },
    chunksSortMode: 'dependency',
  })
));

module.exports = {
  // ...
  plugins: [
    // ...
  ].concat(htmlPlugins),
  // ...
};
```

## Usage

```bash
$ npm run dev
```

And open `localhost:8000/index.html` and `localhost:8000/login.html`
