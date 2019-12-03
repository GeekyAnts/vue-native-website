---
title: Basic Components
type: guide
order: 5
---

### View

The most fundamental component for building a User Interface (UI) are View's. A View is a container that supports layout.
These `Views` are designed to be nested inside other views and can have any amount of child Views inside the parent View. Parent Views can nest any type of child Views inside them.  

A View is kind of like the vue-native equivalant of a `<div>` in HTML.

### Text

A Vue Native component for displaying text. The Text component supports nesting, styling, and touch handling.

```html
<template>
    <view class="text-container">
        <text>Hello World</text>
    </view>
</template>
```

```css
<style>
.text-container {
  flex: 1;
  margin-bottom: 30;
}
</style>
```

### Image

A Vue Native component for displaying different types of images, including network images, static resources, temporary local images, and images from local disk, such as the camera roll.

Here we can see that we are dynamically setting the `source` attribute of each image using the `v-bind` shorthand syntax "`:`". We also `v-bind` to the `style` property and pass in an object with a couple key-value pairs of styles we want to apply.

```html
<template>
    <view>
        <image
          :source="require('/vue-native/img/favicon.png')"
        />
        <image
          :style="{width: 50, height: 50}"
          :source="{uri: 'https://facebook.github.io/react-native/docs/assets/favicon.png'}"
        />
        <image
          :style="{width: 66, height: 58}"
          :source="{uri: 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADMAAAAzCAYAAAA6oTAqAAAAEXRFWHRTb2Z0d2FyZQBwbmdjcnVzaEB1SfMAAABQSURBVGje7dSxCQBACARB+2/ab8BEeQNhFi6WSYzYLYudDQYGBgYGBgYGBgYGBgYGBgZmcvDqYGBgmhivGQYGBgYGBgYGBgYGBgYGBgbmQw+P/eMrC5UTVAAAAABJRU5ErkJggg=='}"
        />
    </view>
</template>
```

### TextInput

A foundational component for inputting text into the app via a keyboard. Props provide configurability for several features, such as auto-correction, auto-capitalization, placeholder text, and different keyboard types, such as a numeric keypad.

In this example, we again take advantage of the `v-bind` directive, as well as a new one. The `v-model` directive. We will come back to this directive in just a bit, but for now just know that `v-model` directive allows us to set up an awesome concept known as `Two-Way Data Binding`.

```html
<template>
    <text-input
        :style="{height: 40, width: 100, borderColor: 'gray', borderWidth: 1}"
        v-model="text"
      />
</template>
```

```js
<script>
    export default {
        data: function() {
            return {
                text: ''
            };
        }
    }
</script>
```

### ScrollView

A component that wraps the platform in ScrollView while providing integration with the touch locking "responder" system. ScrollView simply renders all its react child components at once. That makes it very easy to understand and use.

Keep in mind that ScrollViews must have a bounded height in order to work, since they contain unbounded-height children into a bounded container (via a scroll interaction).


```html
<template>
    <scroll-view :content-container-style="{contentContainer: {
        paddingVertical: 20
    }}">
        <!-- Content goes here -->
    </scroll-view>
</template>
```

### Button

A basic button component that should render nicely on any platform. Supports a minimal level of customization.
We can do more than just bind to data and style views with Vue Directives. 

This button has an event handler `on-press` that we are binding to. When that event gets fired, we run a method on our Vue Instance.

```html
<template>
    <button
        :on-press="onPressLearnMore"
        title="Learn More"
        color="#841584"
        accessibility-label="Learn more about this purple button"
    />
</template>
```

```js
<script>
export default {
    methods: {
        onPressLearnMore: function() {
            alert('Hello')
        }
    }
}
</script>
```

### FlatList

A FlatList is a performant interface for rendering simple flat lists, supporting the most handy features:  

- Fully cross-platform.
- Optional horizontal mode.
- Configurable viewability callbacks.
- Header support.
- Footer support.
- Separator support.
- Pull to Refresh.
- Scroll loading.
- ScrollToIndex support.  
  
One of the drawbacks using FlatList is the renderItem method should return JSX with the actual React Native components. We are working on this and a fix should be available soon.

Here we are binding to the data property and passing in an Array containing key-value objects. As well as rendering out the the List in our data that we are binding to and looping through.

```html
<template>
    <flat-list
        :data="[{key: 'a'}, {key: 'b'}]"
        :render-item="(item) => renderList(item)"
    />
</template>
```

```js
<script>
import React from 'react';
import {Text} from 'react-native';
    export default {
        methods: {
            renderList: function(item) {
                return (<Text>{item.item.key}</Text>)
            }
        }
    }
</script>
```

### ActivityIndicator

A component that displays a circular loading indicator. This type of component is great when using in conjunction with a conditional Vue directive such as `v-if` or `v-show`, since we can toggle the visibility based on a boolean value in our Vue Instance data property.
```html
<template>
    <view 
        v-if="isLoading"
        :style="{flex: 1, justifyContent: 'center'}">
        <activity-indicator size="large" color="#0000ff" />
    </view>
</template>
```

### Alert

A component that launches an alert dialog with the specified title and message. You can optionally provide a list of buttons in the alert as well. Tapping any button will fire the respective onPress callback and dismiss the alert. By default the only button rendered, will be an 'OK' button.

Again, we initiate this alert with another method bound to an `on-press` event listener.

```html
<template>
    <button
        :on-press="onPressLearnMore"
        title="Learn More"
        color="#841584"
        accessibility-label="Learn more about this purple button"
    />
</template>
```

```js
<script>
import { Alert } from 'react-native';
export default {
    methods: {
        onPressLearnMore: function() {
            Alert.alert(
                'Alert Title',
                'My Alert Msg',
                [
                    {text: 'Ask me later', onPress: () => console.log('Ask me later pressed')},
                    {text: 'Cancel', onPress: () => console.log('Cancel Pressed'), style: 'cancel'},
                    {text: 'OK', onPress: () => console.log('OK Pressed')},
                ],
                { cancelable: false }
            );
        }
    }
}
</script>
```

### StatusBar

A component that controls the app status bar.

```html
<template>
    <view>
        <status-bar
            background-color="blue"
            bar-style="light-content"
        />
    </view>
</template>
```

### Switch

A component that renders a boolean "on-off" input. Switches are controlled components that require an `on-value-change` callback that updates it's value prop in order for the component to reflect user actions on the Vue Instance.

```html
<template>
    <view style = {styles.container}>
        <switch
            :on-value-change = "handleChange"
            :value = "value"/>
    </view>
</template>
```

```js
<script>
    export default {
        data: function() {
            return {
                value: false
            }
        },
        methods: {
            handleChange: function(val) {
                this.value = val;
            }
        }
    }
</script>
```

The above can also be implemented using `v-model` from `vue-native-template-compiler` version `0.0.10` and above.

```html
<template>
    <view style = {styles.container}>
        <switch v-model="value"/>
    </view>
</template>
```

### TouchableOpacity

A wrapper for making Views respond properly to touch input. On press down, the opacity of the wrapped View is decreased, dimming it.

```html
<template>
    <touchable-opacity :on-press="onPressButton">
      <image
        :style="{alignItems: 'center', backgroundColor: '#DDDDDD'}"
        :source="require('./myButton.png')"
      />
    </touchable-opacity>
</template>
```

```js
<script>
    export default {
        methods: {
            onPressButton: function() {
                alert('Clicked Image')
            }
        }
    }
</script>
```

### WebView

WebView components are special components that render web content in a native View.

```html
<template>
    <web-view
        :source="{uri: 'https://github.com/facebook/react-native'}"
        :style="{marginTop: 20}"
    />
</template>
```

### Further Details

For further details about different components and API's in depth, you can refer to https://facebook.github.io/react-native/
