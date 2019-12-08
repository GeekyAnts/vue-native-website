---
title: Getting Started
type: guide
order: 3
---

## Getting Started

** Hello World In Vue Native **

The easiest way to try out [Vue Native](https://vue-native.io/) is by building a Hello world app. The [Installation](docs/installation.html) page provides setup of installing Vue Native and setup the project.
Create a `App.vue` file and copy and paste the below content.

```html
<template>
  <view class="container">
    <text class="text-color-primary">{{message}}</text>
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

```css
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

**If you use Expo:**

Delete the `App.js` file.

In the file `your-app/node-modules/expo/AppEntry.js` (not in `your-app/node-modules/@expo/AppEntry.js`)

change 

```
import App from '../../App'; 
```

to 

```
import App from '../../App.vue';
```

<div class="hello-world-container">
  <div class="hello-world-wrapper">
    <img src="/images/helloWorld.png" class="img-wrapper" />
  </div>
</div>
