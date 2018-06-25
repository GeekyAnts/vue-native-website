---
title: Animation
type: guide
order: 9
vue_version: 2.5.13
---

Animations are very important to create a great user experience. Animations allow you to convey physically believable motion in your interface. The Animated API is designed to make it very easy to concisely express a wide variety of interesting animation and interaction patterns in a very performant way. Here Are Few Examples.

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

## Introduction

### DOM and Vue instance's data binding :

The data that is used under the `data` function property is bound to the one used in the template section. Meaning manipulating this data, enables the corresponding element in the template section to be (re)rendered.

For Example consider these `template` and `script` sections:

```html
<template>
  <view>
    <text>
      Message: {{ msg }}
    </text>
  </view>
</template>
```

```css
<script>
import { Text, View } from "react-native";
export default {
  data: function() {
    return {
      msg: "Vue Native!"
    };
  }
};
</script>
```

In the above code snippet, changing the `msg` property would (re)render the `text` component.

It is important to understand this concept because when we provide the animation values, this feature enables us to not use setState as we do in React Native and the manipulation of the DOM happens under the hood.

### React Native Animated API

To animate the components, make use of the Animated API provided by the `react-native` package.

Some of the important Animation types used in this article :

#### Animated.timing()

This is the most commonly used Animation type. It supports animating a value over time using one of various predefined easing functions, or you can use your own. To get an idea of it must be used :

```
Animated.timing(msg, {
  toValue: 100,
  easing: Easing.back(),
  duration: 2000,
}).start();
```

#### Composing Animations

Animations can be combined and played in sequence or in parallel.

##### Sequence and Parallel types

Sequential animations can play a set of given animations immediately after the previous animation has finished, or they can start after a specified delay.

Parallel animations, like their name suggests, executes the animations provided parallely. If one animation is stopped or interrupted, then all other animations in the group are also stopped.

```
Animated.sequence([
  Animated.parallel([
    // after decay, in parallel:
    Animated.spring(position, {
      toValue: {x: 0, y: 0}, // return to start
    }),
    Animated.timing(twirl, {
      // and twirl
      toValue: 360,
    }),
  ]),
]).start();
```

#### Interpolation

Another important feature we are going to be using is the `Interpolation` .
Each property can be run through an interpolation first. An interpolation maps input ranges to output ranges, typically using a linear interpolation but also supports easing functions.

A simple mapping to convert a 0-1 range to a 0-100 range would be:

```
value.interpolate({
  inputRange: [0, 1],
  outputRange: [0, 100],
});
```

## Animations in Vue-Native using Animated API

### The Grow Effect

The `template` section consists of an `Animated:view` with style that consists of variable associated with animation.

```html
<template>
  <view class="container" >
      <Animated:View
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

`growth` is the variable that is provided with the animation values and it is defined as shown below. Also we make use of several functions provided by Vue such as `created` to initialise our values, `data` function to define the data that will be used in our templates and functions, `mounted` to call the function to animate our component, `components` consists of all the components used in the `template` and finally the `methods` sections which contain all the functions.

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
    this.animategrowth();
  },
  components: {
    View,
    Easing
  },
  methods: {
    animategrowth: function() {
      this.growthValue.setValue(0);
      Animated
        .timing(this.growthValue, {
          toValue: 1,
          duration: 1000,
          easing: Easing.linear
        })
        .start(() => {
          this.animategrowth();
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

From the above code, we can see a function named `animategrowth` which makes use of the Animated APIs we spoke about earlier.

The callback used inside the `start` function is used to repeat the animation.

`interpolate` is used to interpolate the values corresponding to the `input` and `output` range.

As the value of `growth` changes, it is updated on the UI because of the DOM and Vue instance data binding which was explained earlier.

<div class="hello-world-container">
  <div class="hello-world-wrapper">
    <img src="/images/grow-animation.gif" class="img-wrapper" />
  </div>
</div>
