---
title: Handling user input
type: guide
order: 7
vue_version: 2.5.13
gz_size: "30.67"
---

To let users interact with your app, we can use the `v-bind` directive to attach event listeners that invoke methods on our Vue Native instances:

``` html
<view class="container">
  <button v-bind:onPress="handleBtnClickCount" :title="btnTitle" />
  <text class="text-container">{{btnClickCount}}</text>
</view>
```
``` js
<script>
export default {
  data: function() {
    return {
      btnTitle: "Click Me",
      btnClickCount: 0,
    };
  },
  methods: {
    handleBtnClickCount: function() {
      this.btnClickCount = this.btnClickCount + 1;
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
.text-container {
  color: blue;
  padding: 2;
  font-size: 20;
}
</style>
```

<div class="hello-world-container">
  <div class="hello-world-wrapper">
    <img src="/images/btn_click_counter_demo.gif" class="img-wrapper" />
  </div>
</div>

Note that in this method we update the state of our app when ever the user click on the button, and Vue Native internally talk with the React Native to update the UI Elements

Vue Native also provides the `v-model` directive that makes two-way binding between form input and app state a breeze:

``` html
<view class="container">
    <text-input
      class="text-input-container"
      placeholder="Type here to translate!"
      v-model="textContent"
    />
    <text class="text-container">{{textContent}}</text>
</view>
```
``` js
<script>
export default {
  data: function() {
    return {
      textContent: ""
    };
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
.text-container {
  color: blue;
  padding: 2;
  font-size: 22;
}
.text-input-container {
  width: 300;
  height: 40;
  font-size: 22;
  border-color: gray;
}
</style>
```

<div class="hello-world-container">
  <div class="hello-world-wrapper">
    <img src="/images/v-model-input.gif" class="img-wrapper" />
  </div>
</div>