---
title: How does it work?
type: guide
order: 15
vue_version: 2.5.13
gz_size: "30.67"
---

This is fork of [react-vue](https://github.com/GeekyAnts/vue-native-core)

Vue-native-core is designed to connect React and Vue, which help you run Vue in React.

There are three uses.

- Use the [reactivity system](https://github.com/SmallComfort/react-vue/blob/dev/README.md#reactivity-system) of Vue to observer React component

- Use the [vue-native-scripts](https://github.com/SmallComfort/react-vue/blob/dev/README.md#native) to run Vue component in React Native

### Reactivity System

Thanks to Vue's clear hierarchical design, we can easily pull out the reactivity system (9 KB gzipped), and drive React component rendering.

```
npm install --save vue-native-core
```

```javascript
import React, { Component } from "react";
import Vue, { observer } from "vue-native-core";

const store = new Vue({
  data() {
    return {
      count: 0
    };
  },
  methods: {
    increase() {
      this.count++;
    }
  }
});

@observer
export default class Demo extends Component {
  render() {
    return <h1 onClick={store.increase}>{store.count}</h1>;
  }
}
```

[document](https://github.com/GeekyAnts/vue-native-core/blob/master/packages/vue-native-core/README.md)

### Vue Native Scripts

Introduce [vue-native-scripts](https://github.com/GeekyAnts/vue-native-core/tree/master/packages/vue-native-scripts), which compile and transform the vue component into a react component.
