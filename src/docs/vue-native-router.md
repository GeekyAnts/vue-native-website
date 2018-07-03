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
        Home: { screen: HomeScreen }
    },
    {
        initialRouteName: "Home"
    },
    contentComponent: props => {
      return <SideBarScreen {...props} />;
    }
);

const RootStack = StackNavigator(
  {
    Home: { screen: HomeScreen},
    Drawer: { screen: Drawer },
  },
  {
    initialRouteName: 'Home',
  }
);
```

## Tab Navigation

Possibly the most common style of navigation in mobile apps is tab-based navigation.
You can use `createBottomTabNavigator` API to implement tab based routing.

```
export default createBottomTabNavigator({
  Home: HomeScreen
});
```

## Further Information

Since the app is based on React Navigation. You can use all the API's specified in react navigation docs. https://reactnavigation.org/docs/en/api-reference.html
