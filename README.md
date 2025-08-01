# @esctn/vue-tsc-api

A (very) simple wrapper that exposes vue-tsc's programmatic API for use in build tools and other TypeScript-related tooling.

## Why does this package exist?

The vue-tsc maintainers have [intentionally](https://github.com/vuejs/language-tools/pull/5528#issuecomment-3092559277) kept vue-tsc as a CLI-only tool to maintain its single purpose and avoid confusion. However, some build tools and TypeScript checkers (like [fork-ts-checker-webpack-plugin](https://github.com/TypeStrong/fork-ts-checker-webpack-plugin), [ts-checker-rspack-plugin](https://github.com/rspack-contrib/ts-checker-rspack-plugin)) need programmatic access to vue-tsc's TypeScript compiler to work with Vue SFCs.

The content of this package is literally one line, and if you think that installing an npm package for it is too much, I feel you!

I published it purely for ergonomics — feel free to just copy the file in your project, and use `require.resolve('path/to/your-wrapper.js')`.

## Installation

```bash
npm install @esctn/vue-tsc-api
```
The `typescript@>=5.0.0` and `vue-tsc@~3.0.3` are peer dependencies.

## Usage

The package exports the same api as `typescript/lib/typescript` but with `vue-tsc` patches to support Vue SFC.

### Example with webpack ts-checker

```javascript
const ForkTsCheckerWebpackPlugin = require('fork-ts-checker-webpack-plugin');

module.exports = {
  // ... your webpack config
  plugins: [
    new ForkTsCheckerWebpackPlugin({
      typescript: {
        // Use @esctn/vue-tsc-api instead of regular TypeScript
        typescriptPath: '@esctn/vue-tsc-api'
      }
    })
  ]
};
```

### Example with custom TypeScript checker

```javascript
const typescript = require('@esctn/vue-tsc-api');

// use as a regular TypeScript api
```

## License

ISC

## Contributing

Issues and pull requests are welcome on [GitHub](https://github.com/escaton/vue-tsc-api).

## Related

- [vue-tsc](https://github.com/vuejs/language-tools/tree/master/packages/tsc) - Vue 3 command line Type-Checking tool
- [Volar.js](https://github.com/volarjs/volar.js/tree/master/packages/typescript) - The infrastructure behind `vue-tsc`
- [TypeScript](https://www.typescriptlang.org/) - The TypeScript language and compiler
