---
title: Installation
type: guide
order: 1
vue_version: 2.5.13
gz_size: "30.67"
---

This page will help you install and build your first native app using Vue-Native.

**System Requirements**
* Globally installed [node](https://nodejs.org/en/) >= 6.0
* Globally installed [npm](https://www.npmjs.com/) >= 4.0
* Globally installed [React Native CLI](https://facebook.github.io/react-native/docs/getting-started.html) which allow you to easily create.

## Setup with React Native

** Step 1 Create React Native Project **

```
react-native init AwesomeVueNative
cd AwesomeVueNative
```

** Step 2 Install Vue Native**

```
npm install vue-native-core vue-native-helper --save
npm install vue-native-scripts --save-dev
```

** Step 3 Configure the React Native Packager**

Create `vueTransformerPlugin.js` file to your project's root and specify supported extensions(vue):

```js
// For React Native version 0.52 or later
var upstreamTransformer = require("metro/src/transformer");

// For React Native version 0.47-0.51
// var upstreamTransformer = require("metro-bundler/src/transformer");

// For React Native version 0.46
// var upstreamTransformer = require("metro-bundler/build/transformer");

var vueNaiveScripts = require("vue-native-scripts");
var vueExtensions = ["vue"];

module.exports.transform = function({ src, filename, options }) {
  if (vueExtensions.some(ext => filename.endsWith("." + ext))) {
    return vueNaiveScripts.transform({ src, filename, options });
  }
  return upstreamTransformer.transform({ src, filename, options });
};
```

Add this to your `rn-cli.config.js` (make one to your project's root if you don't have one already):

```js
module.exports = {
  getTransformModulePath() {
    return require.resolve("./vueTransformerPlugin.js");
  },
  getSourceExts() {
    return ["vue"];
  }
};
```

You've successfully setup [Vue Native](http://vuenativedocs.geekydev.com) with your [React Native](https://facebook.github.io/react-native/) app. Now build truly native app which are ready to run on iOS and Android devices.

Check out the [KitchenSink Vue Native App](https://github.com/GeekyAnts/KitchenSink-Vue-Native) an example which demonstrate different usages of [Vue Native](http://vuenativedocs.geekydev.com) and [NativeBase](https://nativebase.io).
