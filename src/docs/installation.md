---
title: Installation
type: guide
order: 1
vue_version: 2.5.13
gz_size: "30.67"
---

This page will help you install and build your first native app using [Vue Native](https://vue-native.io/).

**System Requirements**
* Globally installed [node](https://nodejs.org/en/) >= 6.0
* Globally installed [npm](https://www.npmjs.com/) >= 4.0
* Globally installed [React Native CLI](https://facebook.github.io/react-native/docs/getting-started.html) which will allow you to easily create and initialize projects.
* Globally installed [Expo CLI](https://docs.expo.io/versions/latest/workflow/expo-cli/)

## Setup with Vue Native Cli

[Vue Native Cli](https://github.com/GeekyAnts/vue-native-cli) is the easiest way to start building an application using [Vue Native](https://vue-native.io/).

Assuming that you have globally installed [expo-cli](https://docs.expo.io/versions/latest/workflow/expo-cli/).

** Step 1: Installing Vue Native CLI and Creating a Project **

```
npm install -g vue-native-cli
vue-native init <projectName> // Initializes crna project
vue-native init <projectName> --no-crna // Initializes react-native project
cd <project-name>
```

** Step 2: Running The App **

```
npm start
```
The above command will run your app in development mode with an interactive prompt. To run it without a prompt, use the --no-interactive flag.
Open it in the [Expo app](https://expo.io/) on your phone to view it. It will reload if you save edits to your files, and you will see build errors and logs in the terminal.

```
npm run ios
```

Like npm start, but also attempts to open your app in the iOS Simulator if you're on a Mac and have it installed.

```
npm run android
```

Like npm start, but also attempts to open your app on a connected Android device or emulator. 
Requires an installation of Android build tools (see [React Native docs](https://facebook.github.io/react-native/docs/getting-started.html) for detailed setup).


## Setup with React Native

 **Note: For RN > 0.55.4. The rn-cli.config.js and vueTransformerPlugin.js should be similar to [rn-cli.config.js](https://github.com/GeekyAnts/vue-native-starter-app/blob/feat/RN58/rn-cli.config.js) and [vueTransformerPlugin.js](https://github.com/GeekyAnts/vue-native-starter-app/blob/feat/RN58/vueTransformerPlugin.js)**


** Step 1: Create React Native Project **

```
react-native init <projectName> --version <version> /* Version should be <= 0.55.4
cd <projectName>
```

** Step 2: Install Vue Native**

```
npm install vue-native-core vue-native-helper --save
npm install vue-native-scripts --save-dev
```

** Step 3: Configure the React Native Packager**

Create `vueTransformerPlugin.js` in your project's root directory and specify supported extensions (vue):

```js
// For React Native version 0.52 or later
var upstreamTransformer = require("metro/src/transformer");

// For React Native version 0.47-0.51
// var upstreamTransformer = require("metro-bundler/src/transformer");

// For React Native version 0.46
// var upstreamTransformer = require("metro-bundler/build/transformer");

var vueNativeScripts = require("vue-native-scripts");
var vueExtensions = ["vue"];

module.exports.transform = function({ src, filename, options }) {
  if (vueExtensions.some(ext => filename.endsWith("." + ext))) {
    return vueNativeScripts.transform({ src, filename, options });
  }
  return upstreamTransformer.transform({ src, filename, options });
};
```

Add the following to `rn-cli.config.js` (make one in your project's root directory if you don't have one already):

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

You've successfully set up [Vue Native](https://vue-native.io/) with your [React Native](https://facebook.github.io/react-native/) app! 
You can now build truly native apps which are ready to run on iOS and Android devices.

Check out the [KitchenSink Vue Native App](https://github.com/GeekyAnts/KitchenSink-Vue-Native) for an example which demonstrates different usages of [Vue Native](https://vue-native.io/) and [NativeBase](https://nativebase.io).

** Step 4: Create A Vue File **
Remove the Content of the `App.js` file and rename `App.js` file with `App.vue`.

Now copy and paste the below code:

```
<template>
  <view class="container">
    <text class="text-color-primary">My Vue Native App</text>
    </view>
</template>

<style>
.container {
  background-color: white;
  align-items: center;
  justify-content: center;
  flex: 1;
}
.text-color-primary {
  color: blue;
}
</style>

```

** Step 5: Running The App **

```
react-native run-ios
```

 The above command will open your app in the iOS Simulator if you're on a Mac and have it installed.

```
react-native run-android
```

 The above command will open your app in the Android Emulator if you have properly setup android studio and emulator.


For more details on getting started with React Native, please refer to [Getting Started With React Native Docs](https://facebook.github.io/react-native/docs/getting-started.html)  