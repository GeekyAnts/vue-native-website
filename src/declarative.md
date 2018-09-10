---
title: Declarative Rendering
type: guide
order: 4
---

At the core of Vue Native is a system that enables us to declaratively render data using straightforward template syntax:

``` html
<template>
  <view>
    <text>{{ message }}</text>
  </view>
</template>
```
```JS
<script>
export default {
  data: function() {
    return {
      message: "Hello World"
    };
  }
};
</script>
```

We have already created our very first `Vue Native` app! This looks pretty similar to rendering a string template, but under the hood a lot work is been done. The data and the native UI elements are now linked, and everything is now **reactive**.

In addition to text interpolation, we can also bind element attributes like this:

``` html
<template>
  <view>
    <button v-bind:title="message" v-bind:on-press="handleBtnPress"/>
  </view>
</template>
```
```JS
<script>
export default {
  data: function() {
    return {
      message: "Hello World"
    };
  },
  methods: {
    handleBtnPress: function() {
      alert('Btn Press');
    }
  }
};
</script>
```

Here we are encountering something new. The `v-bind` attribute you are seeing is called a **directive**. Directives are prefixed with `v-` to indicate that they are special attributes provided by Vue Native, which internal bind with the React Native props and as you may have guessed, they apply special reactive behavior in re-rendering. Here, it is basically saying "keep this element's `title` attribute up-to-date with the `message` property on the Vue instance."

<div class="hello-world-container">
  <div class="hello-world-wrapper">
    <img src="/images/btn_helloWorld.png" class="img-wrapper" />
  </div>
  <div class="hello-world-wrapper">
    <img src="/images/btn_helloWorld_press.png" class="img-wrapper" />
  </div>
</div>
