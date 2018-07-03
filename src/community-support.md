---
title: Community Support
type: guide
order: 7
vue_version: 2.5.13
gz_size: "30.67"
---

## Icons

Usage of icons in Vue Native.

• Import and use the already available icons from the `@expo/vector-icons` for CRNA projects or `react-native-vector-icons` for no-crna projects(remember to link).
• Use PNGs as icons to get your own customized icons running.

We will be showing both these methods here.

### @expo/vector-icons

First install the React Native Elements package using the following command:

```shell
npm install @expo/vector-icons
```

Then you simply import it inside your `script` section like this:

```js
import { Ionicons } from "react-native-elements";
```

Also add the `Ionicons` imported in the `components` block.

```js
<script>
import { Ionicons } from "@expo/vector-icons";
export default {
  components:{Ionicons},
}
</script>
```

If you want to use the imported `Ionicons` globally, you will have to import the `Vue` component from the `vue-native-core` library which is already there if you created your project using the `vue-native-cli`.

Use the `Vue.component` function to specify the component that will be used globally.

```js
import Vue from "vue-native-core";
Vue.component("ionicons", Ionicons);
```

Now you are ready to use the kebab-case equivalent of the import in your `template` with the desired icon.

```html
<template>
  <view class="container">
    <ionicons name="md-checkmark-circle" size=92 color="green" />
  </view>
</template>
```

### Icon images

If you know how to use the React Native `<Image>` component this will be a breeze.

```html
<template>
  <view class="container">
    <image
        :source="require('./logo.png')"
        :style="{width: 100, height: 100}"
      />
  </view>
</template>
```

## Maps

A Map component that uses Apple Maps or Google Maps on iOS and Google Maps on Android.

For non-crna Vue-Native projects, use the `react-native-maps` and link them.

For Vue-Native projects created with Crna, mapView from `expo` can be diretly used as shown below :

```html
<template>
  <view  class="container">
    <map-view class="container"
        :initialRegion="{
          latitude: coordinates.latitude,
          longitude: coordinates.longitude,
          latitudeDelta: coordinates.latitudeDelta,
          longitudeDelta:coordinates.longitudeDelta,
        }"
      />
  </view>
</template>

<script>
import { MapView } from "expo";
export default {
    data: function() {
    return {
      coordinates: {
        latitude: 12.91074,
        longitude: 77.5996363,
        latitudeDelta: 0.0922,
        longitudeDelta: 0.0421
      }
    };
  },
   components: {
    MapView
  }
};
</script>
<style>
.container {
  flex: 1;
}
</style>
```

## Lottie

[Lottie](https://airbnb.design/lottie) is the animation library from AirBnB and Expo has the default support it.

```html
<view class="container">
    <lottie
      ref="lottieAnimation"
      :style="{
        width: 400,
        height: 400,
        backgroundColor: '#eee',
      }"
      :source="animation ? animation  : {}"
    />
    <view class="button-container">
        <button title="Start Animation" :onPress="playAnimation" />
    </view>
</view>
```

```JS
<script>
import lottieAnimationJson from "./lottieAnimation.json";
import { DangerZone } from "expo";
const { Lottie } = DangerZone;

export default {
  components: { Lottie },
  data: function() {
    return {
      animation: null
    };
  },
  methods: {
    async loadAnimationAsync() {
      try {
        const lottieAnimationJsonResponse = await fetch(
          "https://cdn.rawgit.com/airbnb/lottie-react-native/635163550b9689529bfffb77e489e4174516f1c0/example/animations/Watermelon.json"
        );
        const parsedJson = await lottieAnimationJsonResponse.json();
        this.animation = parsedJson;

        this.playAnimation();
      } catch (error) {
        console.log(
          "%c some inside loadAnimationAsync ",
          "background: salmon; color: black",
          error
        );
      }
    },
    playAnimation() {
      if (!this.animation) {
        this.loadAnimationAsync();
      } else if (this.$refs.lottieAnimation) {
        this.$refs.lottieAnimation.reset();
        this.$refs.lottieAnimation.play();
      }
    }
  },
  mounted() {
    this.playAnimation();
  },
  beforeUpdate() {
    this.playAnimation();
  }
};
</script>
```

```css
<style>
.container {
  background-color: #fff;
  align-items: center;
  justify-content: center;
  flex: 1;
}
.button-container {
  padding-top: 20;
}
</style>
```

<div class="hello-world-container">
  <div class="hello-world-wrapper">
    <img src="/images/lottie.gif" class="img-wrapper" />
  </div>
</div>

## Native Base

Refer here for [details](https://docs.nativebase.io/docs/GetStarted.html).
