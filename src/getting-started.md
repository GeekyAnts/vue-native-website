---
title: Getting Started
type: guide
order: 3
---

## Getting Started

** Hello World In Vue Native **

The easiest way to try out [Vue Native](https://vue-native.io/) is by building a Hello world app. The [Installation](docs/installation.html) page provides setup of installing Vue Native and setup the project using [vue-native-cli](https://github.com/GeekyAnts/vue-native-cli).

Once you have created a project using `vue-native-cli` and it is up and running on your chosen platform, you can make changes to the `App.vue` file. Making changes and saving should instantly reflect the changes in the running app.

Start off by copying and pasting the following content to `App.vue`:

```html
<template>
  <view class="container">
    <text class="text-color-primary">{{ message }}</text>
    <button title="Press me!" @press="exclaim" />
  </view>
</template>

<script>
export default {
  data() {
    return {
      message: "Hello World"
    };
  },
  methods: {
    exclaim() {
      this.message += "!";
    }
  },
};
</script>

<style>
.container {
  flex: 1;
  background-color: white;
  align-items: center;
  justify-content: center;
}
.text-color-primary {
  color: blue;
  font-size: 30;
}
</style>
```

You should be able to see the changes on your device/simulator's screen.

<br />
<div class="hello-world-container">
  <div class="hello-world-wrapper">
    <img src="/images/helloWorld.png" class="img-wrapper" />
  </div>
</div>

Now you can try and experiment with `App.vue`, or create and import your own `.vue` files and import them into `App.vue`.
