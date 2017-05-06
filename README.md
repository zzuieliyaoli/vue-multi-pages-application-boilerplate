# Vue Multi-pages Application Boilerplate
> A Vue multi-pages application boilerplate which is based on config created by vue-cli

## Usage

```bash
$ git clone repo-url
$ yarn install

$ npm run dev

$ npm run build
```

And open `localhost:8000/index.html` and `localhost:8000/login.html`

When you want to add new page, just do like these:

- create `newPage.html` to `src/`
- create `newPage.entry.js` to `src/`
- put `newPage.entry.js` 's path to `build/entries.js`

```js
module.exports = {
  index: './src/index.entry.js',
  login: './src/login.entry.js',
  newPage: './src/newPage.entry.js',
};
```

## Details

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
