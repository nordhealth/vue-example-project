# vue-example-project

This repo is an example of using [Vue 3](https://vuejs.org/) / [Vite](https://vitejs.dev/) along with [Nord Design System's](https://nordhealth.design/) [components](https://nordhealth.design/components/). Typescript is used, but this is not a necessity for using Vue and Nord together.

This repo can be forked as a starting point for new apps. However, you may wish to undertake the process yourself so that all dependencies are up to date, and you can choose which Vue features you would like to use. The commit history shows the steps taken to integrate Vue and Nord. Those steps are described next.

## Setting up a project from scratch

First initialize a new Vue project. This will ask a series of questions, to determine your project name, and which vue features you would like to use:

```sh
npm init vue@latest
```

Follow any instructions printed in the terminal.

Next install Nord dependencies:

```sh
npm install @nordhealth/components @nordhealth/css --save
```

When complete, open your editor and navigate to the `vite.config` file. You must [configure Vue to support web components](https://vuejs.org/guide/extras/web-components.html#using-custom-elements-in-vue):

```diff
// vite.config.js
import vue from '@vitejs/plugin-vue'

export default {
  plugins: [
-    vue()
+    vue({
+      template: {
+        compilerOptions: {
+          // treat all tags with a dash as custom elements
+          isCustomElement: (tag) => tag.includes('-')
+        }
+      }
+    })
  ]
}
```

In your `main.js` or `main.ts` file, import the Nord dependencies:

```js
// main.js
import { createApp } from "vue";
import App from "./App.vue";
import "@nordhealth/css";
import "@nordhealth/components";

createApp(App).mount("#app");
```

This will ensure Nord styles are included in your app, and register all web components ready for use.

Now everything is ready! In a component file (assuming use of single-file components and composition API), you can start using Nord:

```vue
<script setup>
import { ref } from "vue";

const name = ref("");
const count = ref(0);
</script>

<template>
  <nord-input label="Your name" v-model="name"></nord-input>
  <p>{{ name }}</p>

  <nord-button variant="primary" @click="count++">
    Count: {{ count }}
  </nord-button>
</template>
```

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=johnsoncodehk.volar) (and disable Vetur) + [TypeScript Vue Plugin (Volar)](https://marketplace.visualstudio.com/items?itemName=johnsoncodehk.vscode-typescript-vue-plugin).

## Type Support for `.vue` Imports in TS

TypeScript cannot handle type information for `.vue` imports by default, so we replace the `tsc` CLI with `vue-tsc` for type checking. In editors, we need [TypeScript Vue Plugin (Volar)](https://marketplace.visualstudio.com/items?itemName=johnsoncodehk.vscode-typescript-vue-plugin) to make the TypeScript language service aware of `.vue` types.

If the standalone TypeScript plugin doesn't feel fast enough to you, Volar has also implemented a [Take Over Mode](https://github.com/johnsoncodehk/volar/discussions/471#discussioncomment-1361669) that is more performant. You can enable it by the following steps:

1. Disable the built-in TypeScript Extension
   1. Run `Extensions: Show Built-in Extensions` from VSCode's command palette
   2. Find `TypeScript and JavaScript Language Features`, right click and select `Disable (Workspace)`
2. Reload the VSCode window by running `Developer: Reload Window` from the command palette.

## Customize configuration

See [Vite Configuration Reference](https://vitejs.dev/config/).

## Project Setup

Clone this repo, then:

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Type-Check, Compile and Minify for Production

```sh
npm run build
```

## Can I use Nord in my own project?

Nord Design System is solely meant for building digital products and experiences for [Nordhealth](https://nordhealth.com/). Please see [LICENSE](LICENSE.md) for full license details.

## Getting support

If you experience any issues while getting started with any of Nord’s tools, please head over to the [Support page](https://nordhealth.design/help/) for more guidelines and help.

## Copyright

Copyright © 2022 Nordhealth Ltd.
