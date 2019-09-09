---
title: Vue Native Router
type: guide
order: 15
vue_version: 2.5.13
gz_size: "30.67"
---

## Navigation in apps

Very soon you'll find yourself in a position where your app has become large enough to have more than a few screens. At this point you'll need a way to navigate between them. It would be nice to have some mechanism to move between screens while keeping track of which screens you visited, where you came from and maybe even a drawer to quickly go to a specific screen.

[Vue Native Router](https://github.com/GeekyAnts/vue-native-router) takes care of these requirements. It provides utilities to create navigators like stack navigators and drawer navigators, and a Vue plugin for easily controlling navigation from within components.

Since it's based on [React Navigation](https://reactnavigation.org/), most of the API and components provided by it can be used in Vue Native.

## Installation

You can install the package using the command
```
$ npm install vue-native-router
```

** NOTE **

Some of its dependencies assume that the following packages are already installed:
- [react-native-reanimated](https://github.com/kmagiera/react-native-reanimated)
- [react-native-gesture-handler](https://github.com/kmagiera/react-native-gesture-handler)
- [react-native-paper](https://github.com/callstack/react-native-paper)

So if you don't have them installed, use this command to install them:

```
$ npm install -g react-native-reanimated react-native-gesture-handler react-native-paper
```

An additional step is required to link these dependencies if you are using just React Native 0.59 without Expo. Refer to [this](https://reactnavigation.org/docs/en/getting-started.html#installation) article for details.

## Basic navigation with a stack navigator

A stack navigator provides a way for your app to transition between screens in such a way that each new screen is placed on top of a stack. `createStackNavigator` makes such a navigator for us. Here is a code snippet that shows how you can use a stack navigator in your app with two screens.

```html
<template>
  <app-navigator></app-navigator>
</template>

<script>
import {
  createAppContainer,
  createStackNavigator,
} from "vue-native-router";

import HomeScreen from "./screens/HomeScreen.vue";
import DetailsScreen from "./screens/DetailsScreen.vue";

const StackNavigator = createStackNavigator(
  {
    Home: HomeScreen,
    Details: DetailsScreen,
  },
  {
    initialRouteName: 'Home',
  }
);

const AppNavigator = createAppContainer(StackNavigator);

export default {
  components: { AppNavigator },
}
</script>
```

** IMPORTANT **

Although there are several navigators provided by `vue-native-router`, the top level navigator must always be wrapped in an app container.

## Moving between screens

Since the navigation is available as prop within the child components. We can use something like `this.navigation.navigate("Home");` to switch from one screen to another.
You can also pass data to routes when we navigate as follows

```js
this.navigation.navigate("RouteName", {/* options go here */});
```

```html
<!-- screens/DetailsScreen.vue -->

<template>
  <view class="container">
    <text>This is the App Details screen</text>
    <button title="Go to home screen" @press="goToHomeScreen"></button>
  </view>
</template>

<script>
export default {
  // Declare `navigation` as a prop
  props: {
    navigation: {
      type: Object
    }
  },
  methods: {
    goToHomeScreen() {
      this.navigation.navigate("Home");
    }
  }
}
</script>
```

### Going back

It is possible to go back from the active screen if there is any. We can trigger it using `this.navigation.goBack()`.

For the full code with usage of `createStackNavigator` refer to [this example](https://github.com/GeekyAnts/vue-native-router/tree/master/examples/example-1-stack-navigator-usage).

## Drawer navigation

For Drawer support, you just need to add screen `Drawer` in `createStackNavigator` options.
You can initialize the drawer using `createDrawerNavigator` and create a sidebar component to render the sidebar view.

```js
const DrawerNavigator = createDrawerNavigator(
  {
    Home: HomeScreen,
    Details: DetailsScreen
  },
  {
    initialRouteName: 'Home'
  }
);

const StackNavigator = createStackNavigator(
  {
    Drawer: DrawerNavigator,
    Home: HomeScreen,
    Details: DetailsScreen
  }
);

const AppNavigator = createAppContainer(StackNavigator);
```

Then use the `AppNavigator` the same way as shown earlier.

```html
<template>
  <app-navigator></app-navigator>
</template>
```

For the full code with usage of `createDrawerNavigator` refer to [this example](https://github.com/GeekyAnts/vue-native-router/tree/master/examples/example-2-drawer-navigator-usage).

## Tab navigation

Another common style of navigation in mobile apps is tab-based navigation.
You can use `createBottomTabNavigator` and `createMaterialTopTabNavigator` to implement tab based routing.

```js
import {
  createAppContainer,
  createBottomTabNavigator,
  createMaterialTopTabNavigator,
  createStackNavigator
} from "vue-native-router";

// An iOS style bottom tab-bar navigator
const BottomTabNavigator = createBottomTabNavigator(
  {
    Details: DetailsScreen,
    Settings: SettingsScreen
  }
);

// An Android style top tab-bar navigator
const MaterialTopTabNavigator = createMaterialTopTabNavigator(
  {
    Details: DetailsScreen,
    Settings: SettingsScreen
  }
);

// The navigators can be used as regular screens in any other navigator
const StackNavigator = createStackNavigator(
  {
    Home: HomeScreen,
    IOSTabs: BottomTabNavigator,
    AndroidTabs: MaterialTopTabNavigator
  }
);

const AppNavigator = createAppContainer(StackNavigator);
```

For the full code with usage of `createBottomTabNavigator` and `createMaterialTopTabNavigator` refer to [this example](https://github.com/GeekyAnts/vue-native-router/tree/master/examples/example-3-tab-navigator-usage).

## Further information

Since the app is based on React Navigation v3, you can use most the API's specified in the react navigation docs at https://reactnavigation.org/docs/en/getting-started.html.

[Vue Native KitchenSink](https://github.com/GeekyAnts/KitchenSink-Vue-Native) is an sample app which uses Vue Native Router and demonstrates [Native Base](https://nativebase.io/) component usage in Vue Native apps.
