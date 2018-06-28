---
title: Device APIs
type: guide
order: 11
vue_version: 2.5.13
---

Some of the functionalities that an app needs that depends on the hardware of the device such as `accelerometer`, `location`, `camera` among many others may be accessed and used as shown in this documentation.

## Accelerometer

Vue-native projects, need to import the `sensors` from `expo`.

```shell
npm i expo
```

```js
import { Accelerometer } from "expo";
```

Let's initialse our `accelerometerData` and bind it to our `template`.

```js
data: function() {
    return {
      accelerometerData: {}
    };
  },
```

```html
<template>
  <view class="container">
      <text>Accelerometer:</text>
        <text>{{accelerometerData.x}}</text>
        </view>
</template>
```

Use the `Accelerometer` and methods provided to listen to changes in the device's accelerometer and store them in `accelerometerData`.

```js
Accelerometer.addListener(accelerometerData => {
  this.accelerometerData = accelerometerData;
});
```

You can even set the update interval of the accelerometer.

```
Accelerometer.setUpdateInterval(1000);
```

Refer the expo [documention](https://docs.expo.io/versions/latest/sdk/accelerometer) for more details.

## Geolocation

Accessing the device's hardware to get to know it's location can be acheived by using APIs provided by `expo`.

You must request permission to access the user's location before attempting to get it. To do this, you will want to use the Permissions API. You can see this in practice in the following example.

```html
<template>
  <view class="container">
        <text>Location:</text>
        <text>{{location.latitude}}</text>
        <touchable-opacity :onPress="getLocationAsync" >
            <text>get location</text>
          </touchable-opacity>
      </view>
</template>

 <script>
import { Constants, Location, Permissions } from "expo";

export default {
  data: function() {
    return {
      location: {},
      errorMessage: ""
    };
  },
  methods: {
    getLocationAsync: function() {
      Permissions.askAsync(Permissions.LOCATION).then(status => {
        if (status !== "granted") {
          errorMessage = "Permission to access location was denied";
        }
        Location.getCurrentPositionAsync({}).then(location1 => {
          location = location1;
        });
      });
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
.text-color-primary {
  color: blue;
}
</style>
```
