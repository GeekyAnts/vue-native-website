---
title: Composing with components
type: guide
order: 6
vue_version: 2.5.13
gz_size: "30.67"
---

The component system is another important concept in Vue Native, because it's an abstraction that allows us to build large-scale applications composed of small, self-contained, and often reusable components. If we think about it, almost any type of application interface can be abstracted into a tree of components:

![Component Tree](/images/components.png)

In Vue Native, registering a component is straightforward, you can simply declare the component in the `components` property:

create a `todoItem.vue` file
``` html
<template>
  <text> {{item.id}}. {{item.text}} </text>
</template>
```
```js
<script>
export default {
  props: {
    item: {
      Type: Object
    }
  }
};
</script>
```

create another `.vue file` and import the above `todoItem` components
```html
<template>
  <view class="container">
  <!--
    Now we provide each todo-item with the todo object
    it's representing, so that its content can be dynamic.
    We also need to provide each component with a "key",
    which will be explained later.
  -->
    <todo-item
      class="text-container"
      v-for="todo in todos"
      :key="todo.text"
      :item="todo"
    />
  </view>
</template>
```
```js
<script>
import TodoItem from "./todoItem";
export default {
  components: { TodoItem },
  data: function() {
    return {
      todos: [
        { id: 1, text: "Learn JavaScript" },
        { id: 2, text: "Learn Vue" },
        { id: 3, text: "Build something awesome" }
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
    <img src="/images/todo_item.png" class="img-wrapper" />
  </div>
</div>

This is a contrived example, but we have managed to separate our app into two smaller units, and the child is reasonably well-decoupled from the parent via the props interface. We can now further improve our `<todo-item>` component with more complex template and logic without affecting the parent app.

In a large application, it is necessary to divide the whole app into components to make development manageable. We will talk a lot more about components, but here's an (imaginary) example of what an app's template might look like with components:

``` html
<view>
  <app-nav></app-nav>
  <app-view>
    <app-sidebar></app-sidebar>
    <app-content></app-content>
  </app-view>
</view>
```