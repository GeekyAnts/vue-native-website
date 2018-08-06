---
title: Vue Native Router
type: guide
order: 15
vue_version: 2.5.13
gz_size: "30.67"
---

## Instructions

To let users handle the routing, We've provided a vuejs plugin [Vue Native Router](https://github.com/GeekyAnts/vue-native-router). It's based on [React Navigation](https://reactnavigation.org/)
You can use install the package using the command `npm install vue-native-router`
Here's the sample app where we have used the plugin [KitchenSink](https://github.com/GeekyAnts/KitchenSink-Vue-Native)

```html
<template>
  <app-navigation></app-navigation>
</template>
```

```js
<script>
import { StackNavigator } from "vue-native-router";
import HomeScreen from "../src/screens/homeScreen.vue";
import DetailsScreen from "../src/screens/detailsScreen.vue";
const AppNavigation = StackNavigator(
  {
    Home: HomeScreen,
    Details: DetailsScreen,
  },
  {
    initialRouteName: 'Home',
  }
);
export default {
    components: { AppNavigation }
}
</script>
```

## Moving in between screens

Since the navigation is available as prop within the child components. We can use something like `this.navigation.navigate("Home");` to switch from one screen to another.
You can also pass data to routes when we navigate. The syntax is `this.navigation.navigate("RouteName", {/* params go here */ });`

```js
<script>
export default {
  props: {
    navigation: {
      type: Object
    }
  },
  methods: {
    handleLetGoBtnPress: function() {
      this.navigation.navigate("Home");
    }
  }
}
</script>
```

### Going back

It is possible to go back from the active screen if there is any. We can trigger it using `this.navigation.goBack()`.

## Drawer Navigation

For Drawer support, you just need to add screen `Drawer` in StackNavigator options.
You can initialize the drawer using DrawerNavigator API and create a sidebar component to render the sidebar view.

```
const Drawer = DrawerNavigator(
  {
    Home: HomeScreen
  },
  {
    initialRouteName: "Home",
  }
);
const AppNavigation = StackNavigator(
  {
    Drawer: Drawer
  },
  {
    initialRouteName: "Drawer"
  }
);
```

Then use the `AppNavigation` the same way shown earlier.

```html
<template>
  <app-navigation></app-navigation>
</template>
```

## Tab Navigation

Possibly the most common style of navigation in mobile apps is tab-based navigation.
You can use `TabNavigator` API to implement tab based routing.

```
const tabNav = TabNavigator(
  {
    Home: HomeScreen,
    Details: DetailsScreen
  },
  {
    tabBarPosition: "bottom",
    tabBarComponent: TabBarBottom
  }
);
```

`tabNav` is then used in our `template` after mentioning it under `components`.

```js
components: {
  tabNav;
}
```

```html
<template>
  <view>
    <tab-nav></tab-nav>
  </view>
</template>
```

## Further Information

Since the app is based on React Navigation v1. You can use all the API's specified in react navigation docs. https://v1.reactnavigation.org/docs/getting-started.html
