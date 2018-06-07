---
title: Basic Components
type: guide
order: 11
vue_version: 2.5.13
gz_size: "30.67"
---

### View
The most fundamental component for building a UI, View is a container that supports layout
`View` is designed to be nested inside other views and can have 0 to many children of any type.

### Text
A Vue Native component for displaying text.

Text supports nesting, styling, and touch handling.

```
<template>
    <view class="text-container">
        <text>Hello World</text>
    </view>
</template>

<style>
.text-container {
  flex: 1;
  margin-bottom: 30;
}
</style>
```

### Image
A Vue Native component for displaying different types of images, including network images, static resources, temporary local images, and images from local disk, such as the camera roll.

```
<template>
    <view>
        <image
          :source={require('/vue-native/img/favicon.png')}
        />
        <image
          :style={width: 50, height: 50}
          :source={uri: 'https://facebook.github.io/react-native/docs/assets/favicon.png'}
        />
        <image
          :style={width: 66, height: 58}
          :source={uri: 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADMAAAAzCAYAAAA6oTAqAAAAEXRFWHRTb2Z0d2FyZQBwbmdjcnVzaEB1SfMAAABQSURBVGje7dSxCQBACARB+2/ab8BEeQNhFi6WSYzYLYudDQYGBgYGBgYGBgYGBgYGBgZmcvDqYGBgmhivGQYGBgYGBgYGBgYGBgYGBgbmQw+P/eMrC5UTVAAAAABJRU5ErkJggg=='}
        />
      </view>
</template>
```

### TextInput
A foundational component for inputting text into the app via a keyboard. Props provide configurability for several features, such as auto-correction, auto-capitalization, placeholder text, and different keyboard types, such as a numeric keypad.

```
<template>
    <text-input
        style={height: 40, borderColor: 'gray', borderWidth: 1}
        v-model="text"
      />
</template>
<script>
    export default {
        data: function() {
            text: ''
        }
    }
</script>
```

### ScrollView
Component that wraps platform ScrollView while providing integration with touch locking "responder" system.

Keep in mind that ScrollViews must have a bounded height in order to work, since they contain unbounded-height children into a bounded container (via a scroll interaction)

ScrollView simply renders all its react child components at once. That makes it very easy to understand and use.

```
<template>
    <scroll-view :content-container-style={contentContainer: {
        paddingVertical: 20
    }}>
        // Content goes here
    </scroll-view>
</template>
```

### Button
A basic button component that should render nicely on any platform. Supports a minimal level of customization.

```
<template>
    <button
        :on-press={onPressLearnMore}
        :title="'Learn More'"
        :color="'#841584'"
        :accessibility-label="'Learn more about this purple button'"
    />
</template>
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
A performant interface for rendering simple, flat lists, supporting the most handy features:

. Fully cross-platform.
. Optional horizontal mode.
. Configurable viewability callbacks.
. Header support.
. Footer support.
. Separator support.
. Pull to Refresh.
. Scroll loading.
. ScrollToIndex support.

One of the drawbacks using Flatlist is the renderItem method should return JSX with the actual React Native components. We are working on this and a fix should be available soon.

```
<template>
    <flat-list
        :data={[{key: 'a'}, {key: 'b'}]}
        :render-item={({item}) => <Text>{item.key}</Text>}
    />
</template>
```

### ActivityIndicator

Displays a circular loading indicator.

```
<template>
    <view :style={flex: 1, justify-content: 'center'}>
        <activity-indicator :size="'large'" :color="'#0000ff'" />
    </view>
</template>
```

### Alert

Launches an alert dialog with the specified title and message.

Optionally provide a list of buttons. Tapping any button will fire the respective onPress callback and dismiss the alert. By default, the only button will be an 'OK' button.

```
<template>
    <button
        :on-press={onPressLearnMore}
        :title="'Learn More'"
        :color="'#841584'"
        :accessibility-label="'Learn more about this purple button'"
    />
</template>
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
```

### StatusBar

Component to control the app status bar.

```
<template>
    <view>
    <status-bar
        background-color="blue"
        bar-style="light-content"
    />
</template>
```

### Switch

Renders a boolean input.

This is a controlled component that requires an `on-value-change` callback that updates the value prop in order for the component to reflect user actions.

```
<template>
    <view style = {styles.container}>
        <switch
            :on-value-change = "handleChange"
            :value = "value"/>
    </view>
</template>
<script>
    export default {
        data: function() {
            return {
                value: false
            }
        },
        methods: {
            handleChange: () => {
                this.value = !this.value
            }
        }
    }
</script>
```

### TouchableOpacity

A wrapper for making views respond properly to touches. On press down, the opacity of the wrapped view is decreased, dimming it.

```
<template>
    <touchable-opacity :on-press="onPressButton">
      <image
        :style={align-items: 'center', background-color: '#DDDDDD'}
        :source={require('./myButton.png')}
      />
    </touchable-opacity>
</template>

<script>
    export default {
        methods: {
            onPressButton: () => {
                alert('Clicked Image')
            }
        }
    }
</script>
```

### WebView

WebView renders web content in a native view.

```
<template>
    <web-view
        :source={uri: 'https://github.com/facebook/react-native'}
        :style={marginTop: 20}
    />
</template>
```