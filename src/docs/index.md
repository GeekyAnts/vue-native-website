---
title: Introduction
type: guide
order: 2
---

First of all we would like to thank SmallComfort (https://github.com/SmallComfort/react-vue) for their efforts in creating the compiler.
## What is Vue Native?
Vue Native is a mobile framework to build truly native mobile app using [Vue.js](https://vuejs.org/). Its is designed to connect [React Native](https://facebook.github.io/react-native) and Vue.js.

Vue Native is a wrapper around React Native APIs, which allows you to use Vue.js and compose rich mobile User Interface.

## What is Vue.js?

Vue (pronounced /vjuː/, like **view**) is a **progressive framework** for building user interfaces. Unlike other monolithic frameworks, Vue is designed from the ground up to be incrementally adoptable. The core library is focused on the view layer only, and is easy to pick up and integrate with other libraries or existing projects.

## What is React Native?
React Native is an open source framework for building truly native mobile application for IOS and Android platform using JavaScript.

## Getting Started

** Hello World In Vue Native **

The easiest way to try out [Vue Native](http://vuenativedocs.geekydev.com) is by building a Hello world app. The [Installation](installation.html) page provides setup of installing Vue Native and setup the project.

Create a .vue file and copy and paste the below content.

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

<div class="hello-world-container">
  <div class="hello-world-wrapper">
    <img src="/images/helloWorld.png" class="img-wrapper" />
  </div>
</div>

## Declarative Rendering

At the core of Vue Native is a system that enables us to declaratively render data using straightforward template syntax:

``` html
<view>
  <text>{{ message }}</text>
</view>
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
<view>
  <button v-bind:title="message" v-bind:on-press="handleBtnPress"/>
</view>
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


## Conditionals and Loops

It's easy to toggle the presence of an element, too:

``` html
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

``` html
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

## Handling User Input

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

## Composing with Components

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

### Relation to Custom Elements

You may have noticed that Vue Native components are very similar to [**React Native Components**](https://facebook.github.io/react-native/docs/getting-started.html). You can use All React Native Component, by making use of the `kebab case (hyphen-delimited)` equivalent components. This is because Vue Native is a wrapper around the React Native APIs.

## Ready for More?

We've have briefly introduced the most basic features of Vue Native - we are making continuous efforts to improve our docs.
Since Vue Native connects React Native and Vue.js, you can also go through [React Native Docs](https://facebook.github.io/react-native/docs/getting-started.html) and [Vue.js Docs](https://vuejs.org/v2/guide/).
