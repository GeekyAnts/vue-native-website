---
title: Community Support
type: guide
order: 6
vue_version: 2.5.13
gz_size: "30.67"
---

## Animations

Animations are very important to create a great user experience. Animations allow you to convey physically believable motion in your interface. The Animated API is designed to make it very easy to concisely express a wide variety of interesting animation and interaction patterns in a very performant way. Here are few examples.

### Introduction

Animations are a useful tool to boost the user experience and hence it must be utilised to the fullest, meaning there are mainly two ways you can animate components:

• To build from ground up, one can use an animation library such as React Native's Animated API and animate components such as `view` or `text`.
• Import animations from animation tools like After Effects (using Lottie).

Let's take a look at how we can achieve the former approach in this section with the help of a simple grow animation.

### The Grow Effect

First, set up the `template` section.

```html
<template>
  <view class="container" >
    <animated:view
     class="growth-animated-view"
        :style="{
          height: growth,
          width: growth ,
          borderRadius:growth,
          }"
    />
  </view>
</template>
```

The template section comprises of an "animated" view and another view wrapped around it. The `animated:view` has inline variable style properties for `height`,`width`, and `borderRadius`. All of these are provided with an animated value `growth` which is intialised when the component is `created`.

All the variable style properties are inline and the others can be provided using the class names as shown below:

```css
<style>
.growth-animated-view {
  background-color: "rgb(0, 138, 231)";
  align-self: center;
}

.container {
  justify-content: center;
  flex: 1;
}
</style>
```

The first step when starting an animation is to know our start and end frames and how the values of the components need to change in order to move from the start frame to the end.

<div style="display: flex;" class="flex-column exam-app">
<div class="card">
  <h4 style="text-align:center">Start frame</h4>
<div class="hello-world-container">
  <div class="hello-world-wrapper">
    <img src="./../images/grow-animation-start.png" class="img-wrapper" />
  </div>
</div>
</div>
<div class="card">
    <h4 style="text-align:center"> End frame</h4>
      <div class="hello-world-container">
  <div class="hello-world-wrapper">
    <img src="./../images/grow-animation-end-frame.png" class="img-wrapper" />
  </div>
</div>
</div>
</div>

In this case, since we are creating a simple "grow" effect on a circular element, our start frame will be an `animated:view` with all the three properties having the value zero. Basically, our start frame will be a blank screen since the `growth` value is set to zero when the component is `created`.

The end frame is a view that has the background color blue and height, width, border radius as 200.

Now the goal is to provide a set of values to `growth` so that the same component is render for each value and appears to "grow".

The `script` section is structured in this manner and the function used is also shown below :

```js
<script>
import { Animated, Easing } from "react-native";

export default {
  data: function() {
    return {
      growth: 0
    };
  },
  created: function() {
    this.growth = new Animated.Value(0);
  },
  mounted: function() {
    this.animateGrowth();
  },
  methods: {
    animateGrowth: function() {

      this.growth.setValue(0);

      Animated.timing(this.growth, {
        toValue: 200,
        duration: 1000,
        easing: Easing.linear
      }).start(() => {
        // this.animateGrowth();
      });
    }
  }
};
</script>
```

The above section has the following functions :

•`created` to initialise our values.
• `data` function to define the data that will be used in our templates and functions.
• `mounted` to call the function to animate our component.
• Finally the `methods` sections which contain all the functions.

`Animated.timing` type from the Animated API is used to provide values to `growth` from 0 to 200 in the duration of 1000 milliseconds. Once this line executes, the `animated.view` starts to show the `growth` effect where it's value gradually increses from 0 to 200 and this is possible without `setstate` because of `Vue`'s DOM and data binding.

This is the result of the above code snippet :

<div class="hello-world-container">
  <div class="hello-world-wrapper">
    <img src="./../images/growAnimation-once.gif" class="img-wrapper" />
  </div>
</div>

`Interpolate` is another feature that can be used to interpolate any value. An interpolation maps input ranges to output ranges, typically using a linear interpolation but also supports easing functions.

In order to reverse this animation, i.e take the component from end frame to the start frame is as easy as interpolating a value. For this purpose , take another value named `growthValue` and use it with the `Animated.timing` as shown below :

```js
<script>
export default {
  data: function() {
    return {
      growthValue: 0,
      growth: 0,
    };
  },
  created: function() {
    this.growthValue = new animated.Value(0);
    this.animatedValueRotate = new animated.Value(0);
  },
  mounted: function() {
    this.animateGrowth();
  },
  methods: {
    animateGrowth: function() {
      this.growthValue.setValue(0);
      Animated
        .timing(this.growthValue, {
          toValue: 1,
          duration: 1000,
          easing: Easing.linear
        })
        .start(() => {
          // this.animateGrowth();
        });
      this.growth = this.growthValue.interpolate({
        inputRange: [0, 0.5, 1],
        outputRange: [0, 200, 0]
      });
    }
  }
};
</script>
```

`growthValue.interpolate` is a simple mapping to convert a 0-1 range to a 0-200 range which produces the following effect :

<div class="hello-world-container">
  <div class="hello-world-wrapper">
    <img src="./../images/growAnimation-single-bounce.gif" class="img-wrapper" />
  </div>
</div>

Now to repeat the same animation, add a recursive call inside the `start` function callback by uncommenting the above code.

<div class="hello-world-container">
  <div class="hello-world-wrapper">
    <img src="./../images/grow-animation.gif" class="img-wrapper" />
  </div>
</div>

Refer the [community support](http://staging-vue-native.geekydev.com/docs/community-support.html) section for more details on how to use animation tools in Vue-native.

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

## Device APIs

Some of the functionalities that an app needs that depends on the hardware of the device such as `accelerometer`, `location`, `camera` among many others may be accessed and used as shown in this documentation.

For non-crna projects created with vue-native, you may use packages such as `react-native-sensors` and link them to get started.

### Accelerometer

Vue-native projects, need to import the `sensors` from `expo`.

```shell
npm i expo
```

```js
import { Accelerometer } from "expo";
```

Let's initialse our `accelerometerData` and bind it to our `template`.

```js
data: function() {
    return {
      accelerometerData: {}
    };
  },
```

```html
<template>
  <view class="container">
      <text>Accelerometer:</text>
        <text>{{accelerometerData.x}}</text>
        </view>
</template>
```

Use the `Accelerometer` and methods provided to listen to changes in the device's accelerometer and store them in `accelerometerData`.

```js
Accelerometer.addListener(accelerometerData => {
  this.accelerometerData = accelerometerData;
});
```

You can even set the update interval of the accelerometer.

```
Accelerometer.setUpdateInterval(1000);
```

Refer the expo [documention](https://docs.expo.io/versions/latest/sdk/accelerometer) for more details.

### Geolocation

Accessing the device's hardware to get to know it's location can be acheived by using APIs provided by `expo`.

You must request permission to access the user's location before attempting to get it. To do this, you will want to use the Permissions API. You can see this in practice in the following example.

```html
<template>
  <view class="container">
        <text>Location:</text>
        <text>{{location.latitude}}</text>
        <touchable-opacity :onPress="getLocationAsync" >
            <text>get location</text>
          </touchable-opacity>
      </view>
</template>

 <script>
import { Constants, Location, Permissions } from "expo";

export default {
  data: function() {
    return {
      location: {},
      errorMessage: ""
    };
  },
  methods: {
    getLocationAsync: function() {
      Permissions.askAsync(Permissions.LOCATION).then(status => {
        if (status !== "granted") {
          errorMessage = "Permission to access location was denied";
        }
        Location.getCurrentPositionAsync({}).then(location1 => {
          location = location1;
        });
      });
    }
  }
};
</script>
```

```css
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

### Camera

For vue-native projects created with CRNA, we will be using `expo`'s `camera` component.

With use of Camera one can also take photos and record videos that are saved to the app's cache. Morever, the component is also capable of detecting faces and bar codes appearing on the preview.

Requires `Permissions.CAMERA`. Video recording requires `Permissions.AUDIO_RECORDING`.

#### Basic Example

```html
<template>
  <view class="container">
          <camera class="container" :type="this.type" v-if="loaded">
          </camera>
    </view>

</template>
```

```js
<script>
import { Camera, Permissions } from "expo";

export default {
 data: function() {
   return {
     hasCameraPermission: false,
     type: Camera.Constants.Type.back,
     loaded: false
   };
 },
 created: function() {},
 mounted: function() {
   Permissions.askAsync(Permissions.CAMERA)
     .then(status => {
       setTimeout(() => {
         this.loaded = true;
       }, 1000);
       console.log(status.status);
       hasCameraPermission = status.status == "granted" ? true : false;
       console.log(hasCameraPermission);
     })
     .catch(err => {
       print(err);
     });
 },
 components: { Camera },
 methods: {}
};
</script>
```

```css
<style>
.container {
  flex: 1;
}
.text-color-primary {
  color: blue;
}
</style>
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
