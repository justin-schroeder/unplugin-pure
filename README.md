# `unplugin-pure`

> This is a fork of Daniel Roe’s [`rollup-plugin-pure`](https://github.com/danielroe/rollup-plugin-pure)

## Features

- ⚡️ avoids end-users bundling unused code

## How it works

Definition functions (for example, in Vue with `defineComponent`) are increasingly common but do not play nice with tree-shaking. It's not possible to tell whether or not a function call which receives an object can be tree-shaken from a build, as it's possible there might be side effects.

Rollup supports `/* #__PURE__ */` annotations to declare this from a library author's point of view, but it can be tricky when we know that _every_ occurrence of a function call is pure.

This plugin will automatically inject the annotation before any occurrence of the function call.

## Installation

Install and add `unplugin-pure` to your Vite or Rollup config.

```bash
pnpm add -D unplugin-pure
```

```js
import { defineConfig } from 'vite'
import { PluginPure } from 'unplugin-pure'

export default defineConfig({
  plugins: [
    PluginPure({
      functions: ['defineComponent'],
      include: [/(?<!im)pure\.js$/],
      // exclude: [],
      // sourcemap: true,
    }),
  ],
})
```

## 💻 Development

- Clone this repository
- Enable [Corepack](https://github.com/nodejs/corepack) using `corepack enable` (use `npm i -g corepack` for Node.js < 16.10)
- Install dependencies using `pnpm install`
- Stub module with `pnpm dev:prepare`
- Run `pnpm dev` to start [playground](./playground) in development mode

## License

Made with ❤️

Published under the [MIT License](./LICENCE).
