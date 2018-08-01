---
title: Testing
type: guide
order: 16
vue_version: 2.5.13
gz_size: "30.67"
---

## Snapshot testing

Snapshot tests are a very useful tool whenever you want to make sure your UI does not change unexpectedly.A typical snapshot test case for a mobile app renders a UI component, takes a screenshot, then compares it to a reference image stored alongside the test. The test will fail if the two images do not match.

A similar approach can be taken when it comes to testing your Vue-Native components. Instead of rendering the graphical UI, which would require building the entire app,you can use a test renderer to quickly generate a serializable value.

Since we want to parse and take a screenshot of `*.vue` files we first read these files and parse them.

Follow the below snippets and add them to the file `*-test.js` under the `__tests__` folder:

• Read the vue file content using node's `fs` package.

```js
var fs = require("fs");
const data = fs.readFileSync("{absolute path to vue file}", "utf8");
```

• Parse the `data` using `vue-native-scripts`' `reactVueTemplateParser` function to extract elements from the vue code.

```js
const Login = reactVueTemplateParser(data);
```

Now use the parsed data to render using the `renderer` from `react-test-renderer`.

```js
describe("Login Component", () => {
  it("renders correctly", () => {
    const tree = renderer.create(<View />).toJSON();
    expect(tree).toMatchSnapshot();
  });
});
```

Run `npm test -- -u` which runs the test and creates a `snapshot` and replaces anything in the `*-test.js.snap` file under the `__snapshots__` folder.

The snapshot created looks something like this :

```js
// Jest Snapshot v1, https://goo.gl/fbAQLP

exports[`Login Component renders correctly 1`] = `
<import __react__vue__Vue, {
  observer as __react__vue__observer
} from 'vue-native-core'
import __react__vue__ReactNative from 'react-native'
import __react__vue__PropType from 'prop-types'
import {
  buildNativeComponent as __react__vue__buildNativeComponent
} from 'vue-native-helper'
import {
  bindNativeClass as __react__vue__bindClass,
  bindNativeStyle as __react__vue__bindStyle,
  mergeNativeStyleAndNativeClass as __react__vue__mergeNativeStyleAndNativeClass,
  mergeProps as __react__vue__mergeProps
} from 'vue-native-helper'
import {
  createElement as __react__vue__createElement,
  Component as __react__vue__Component
} from 'react'

const __react__vue__options = {}

const __react__vue__render = function render(vm) {
  return __react__vue__createElement(vm.$options.components['Text'], __react__vue__mergeProps.call(this, this.props.__react__vue__nativeEvents, {
    ref: ref => {
      this.setRootRef(ref);
      this.props['__react__vue__setRef'] && this.props['__react__vue__setRef'](ref);
    },
    style: __react__vue__mergeNativeStyleAndNativeClass(__react__vue__bindClass.call(this, {
      parentClass: this.props.style
    }), __react__vue__bindStyle(undefined, undefined, undefined))
  }), "abc");
};

const __react__vue__css = {
  "container": {
    "backgroundColor": "white",
    "alignItems": "center",
    "justifyContent": "center",
    "flex": 1
  },
  "text-color-primary": {
    "color": "blue"
  }
}

const __react__vue__ComponentBuilded = __react__vue__buildNativeComponent(__react__vue__render, __react__vue__options, {
  Component: __react__vue__Component,
  PropTypes: __react__vue__PropType,
  Vue: __react__vue__Vue,
  ReactNative: __react__vue__ReactNative,
  css: __react__vue__css
})

export default __react__vue__observer(__react__vue__ComponentBuilded) />
`;
```

The vue file used here looks like this :

```html
<template>
  <text>abc</text>
</template>
```

```css
<style>
.container {
  background-color: black;
  align-items: center;
  justify-content: center;
  flex: 1;
}
.text-color-primary {
  color: blue;
}
</style>
```

Changing anything in the vue file would result in a failed test (`npm test`) since it compares the current image with the snapshot it already has.

Running `npm test -- -u` would replace the snapshot with the updated UI components.
