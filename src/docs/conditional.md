---
title: Conditionals and Loops
type: guide
order: 7
vue_version: 2.5.13
gz_size: "30.67"
---

It's easy to toggle the presence of an element, too:

```html
<view>
  <text v-if="seen">Now you see me</text>
</view>
```

```JS
<script>
export default {
  data: function() {
    return {
      seen: false
    };
  }
};
</script>
```

This example demonstrates that we can bind data, and dynamically manipulate the UI elements.

There are quite a few other directives, each with its own special functionality. For example, the `v-for` directive can be used for displaying a list of items using the data from an Array:

```html
<view class="container">
  <text class="text-container" v-for="todo in todos" :key="todo.text">
    {{ todo.text }}
  </text>
</view>
```

```JS
<script>
export default {
  data: function() {
    return {
      todos: [
        { text: "Learn JavaScript" },
        { text: "Learn Vue" },
        { text: "Build something awesome" }
      ]
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
}
</style>
```

<div class="hello-world-container">
  <div class="hello-world-wrapper">
    <img src="/images/vFor_text_list.png" class="img-wrapper" />
  </div>
</div>
