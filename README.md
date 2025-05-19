# vue-example-project

This repo is an example of using [Vue 3](https://vuejs.org/) with [Vite](https://vitejs.dev/) along with [Nord Design System's](https://nordhealth.design/) [components](https://nordhealth.design/components/). TypeScript is used, but this is not a necessity for using Vue and Nord together.

This repo can be forked as a starting point for new apps. However, you may wish to undertake the process yourself so that all dependencies are up to date, and you can choose which Vue features you would like to use. The steps to integrate Vue and Nord are described next.

## Setting up a project from scratch

First initialize a new Vue project. This will ask a series of questions, to determine your project name, and which Vue features you would like to use:

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
import './assets/main.css';

import { createApp } from 'vue';
import App from './App.vue';

import '@nordhealth/css';
import '@nordhealth/components';

createApp(App).mount('#app');
```

This will ensure Nord styles are included in your app, and register all Web Components ready for use.

To get types and IntelliSense for Nord components in templates of Vue Single-File Components, add the following to your `tsconfig.json` in a TypeScript project, or `jsconfig.json` in a JavaScript project:

```json
{
  "compilerOptions": {
    "types": ["@nordhealth/components/lib/vue.d.ts"]
  }
}
```

Now everything is ready! In a component file (assuming use of Vue Single-File Components and Composition API), you can start using Nord:

```vue
<script setup>
import { ref } from 'vue';

const name = ref('');
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

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur).

## Type Support for `.vue` Imports in TS

TypeScript cannot handle type information for `.vue` imports by default, so we replace the `tsc` CLI with `vue-tsc` for type checking. In editors, we need [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) to make the TypeScript language service aware of `.vue` types.

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

Copyright © 2025 Nordhealth Ltd.
