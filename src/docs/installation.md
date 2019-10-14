---
title: Installation
type: guide
order: 1
gz_size: "30.67"
---

This page will help you install and build your first native app using [Vue Native](https://vue-native.io/).

** System Requirements **
* Globally installed [node](https://nodejs.org/en/) >= 6.0
* Globally installed [npm](https://www.npmjs.com/) >= 4.0
* Globally installed [Expo CLI](https://docs.expo.io/versions/latest/workflow/expo-cli/) **OR** [React Native CLI](https://facebook.github.io/react-native/docs/getting-started.html)

## Setup with Vue Native CLI

[Vue Native CLI](https://github.com/GeekyAnts/vue-native-cli) is the easiest way to start building an application using [Vue Native](https://vue-native.io/).

** Installing Vue Native CLI **

Install Vue Native CLI globally with the following command

```
$ npm install --global vue-native-cli
```

It allows you to setup a fresh Vue Native app with either Expo or React Native CLI. Each come with their own pros and cons.

### For Expo users

Expo was designed to allow developers to quickly set up and develop React Native apps, without having to configure Xcode or Android Studio. It is most suitable for you if you come from a Web background.

** Step 0: Install Expo CLI globally **

```
$ npm install --global expo-cli
```

** Step 1: Create a new project using the CLI's `init` command **

```
$ vue-native init <projectName>
```

Follow the prompts to create a new directory with the specified name.

** <a name="modifying-app-json"></a>NOTE **

At this point you will need to manually change the `app.json` that has been generated inside the new project directory. To make the packager recognize `.vue` files, a `sourceExts` field under `packagerOpts`.

```diff
{
  "expo": {
    "name": "Your app's name",
    "platforms": [
      "ios",
      "android",
      "web"
    ],
    "version": "1.0.0",
    ...
    "packagerOpts": {
+     "sourceExts": ["js", "json", "ts", "tsx", "vue"],
      "config": "metro.config.js"
    }
  }
}
```

** Step 2: Run the app **

Now `cd` into the newly created directory and start the development server.

```
$ cd <projectName>
$ npm start
```

The above command will run your app in development mode with an interactive prompt. To run it without a prompt, use the --no-interactive flag. Open it in the [Expo app](https://expo.io/) on your phone to view it. It will reload if you save edits to your files, and you will see build errors and logs in the terminal.

Alternatively, you can start the app directly on platform simulators.

```
$ npm run ios
```

This works just like `npm start`, but also attempts to open your app in the iOS Simulator if you're on a Mac and have it installed.

```
$ npm run android
```

This works just like `npm start`, but also attempts to open your app on a connected Android device or emulator. It requires an installation of Android build tools (see the [React Native docs](https://facebook.github.io/react-native/docs/getting-started.html) for detailed setup).

### For React Native CLI users

Using Expo to develop your app comes with the disadvantage that you can't work with custom native modules beyond React Native's API, since Expo doesn't build native code. So if you ever need to work with custom Java or Swift modules, you'll need to eject the app with `expo eject`. On the other hand, you can set up your project with React Native CLI, which will allow you to work with such modules from the start.

** Step 0: Install React Native CLI globally **

```
$ npm install --global react-native-cli
```

** Step 1: Create a new project using the CLI's `init` command with the `--no-expo` option **

```
$ vue-native init <projectName> --no-expo
```

Follow the prompts to create a new directory with the specified name.

** Step 2: Run the app **

Now `cd` into the newly created directory and start the development server.

```
$ cd <projectName>
$ npm start
```

You can also use `react-native-cli` to start the app with platform specific options. For example

```
$ react-native run-android
```

would start the development server and the app on a running Android emulator, while

```
$ react-native run-ios --simulator "iPhone 8"
```

would start the development server and the app on an iPhone 8 simulator.

## Configuring a React Native project for Vue Native

** NOTE: React Native <0.59 is no longer supported. If you wish to use Vue Native in a React Native project, you will need to upgrade to at least `react-native` v0.59. **

If you already have a React Native project (either pre-existing or freshly set up) and would like to use Vue Native with it, you can do so with the following steps:

** Step 1: Install Vue Native **

```
$ npm install vue-native-core vue-native-helper --save
$ npm install vue-native-scripts --save-dev
```

`vue-native-core` and `vue-native-helper` contain code that allow Vue Native components to be instantiated and used at run-time. `vue-native-scripts` is a library that transpiles `.vue` single file components and Vue component templates into React components. It is only required as a dev dependency.

** Step 2: Configure the React Native Packager **

Create `vueTransformerPlugin.js` in your project's root directory and specify supported extensions (vue):

```js
// For React Native 0.59 and above
var upstreamTransformer = require("metro-react-native-babel-transformer");

var vueNativeScripts = require("vue-native-scripts");
var vueExtensions = ["vue"];

module.exports.transform = function({ src, filename, options }) {
  if (vueExtensions.some(ext => filename.endsWith("." + ext))) {
    return vueNativeScripts.transform({ src, filename, options });
  }
  return upstreamTransformer.transform({ src, filename, options });
};
```

Add the following to `metro.config.js` (make one in your project's root directory if you don't have one already):

```js
const { getDefaultConfig } = require("metro-config");

module.exports = (async () => {
  const {
    resolver: { sourceExts }
  } = await getDefaultConfig();
  return {
    transformer: {
      babelTransformerPath: require.resolve("./vueTransformerPlugin.js"),
      getTransformOptions: async () => ({
        transform: {
          experimentalImportSupport: false,
          inlineRequires: false,
        },
      })
    },
    resolver: {
      sourceExts: [...sourceExts, "vue"]
    }
  };
})();
```

** Step 2.5: (Only for Expo users) **

Change the contents of `app.json` in the root of your project as described [here](#modifying-app-json)

At this point you've successfully set up [Vue Native](https://vue-native.io/) with your [React Native](https://facebook.github.io/react-native/) app! You can now build truly native apps which are ready to run on iOS and Android devices.

Check out the [KitchenSink Vue Native App](https://github.com/GeekyAnts/KitchenSink-Vue-Native) for an example which demonstrates different usages of [Vue Native](https://vue-native.io/) and [NativeBase](https://nativebase.io).

** Step 3: Create A Vue File **

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

** Step 4: Running The App **

You can now start the development server as usual. If you use Expo, you can simply run

```
$ npm start
```

If you use just React Native, you can also use `react-native` CLI commands. For example,

```
$ react-native run-android
```

the above command will open your app in the Android Emulator if you have properly setup android studio and emulator.


For more details on getting started with React Native, please refer to [Getting Started With React Native Docs](https://facebook.github.io/react-native/docs/getting-started.html)
