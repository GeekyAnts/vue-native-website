---
title: Map View
type: guide
order: 12
vue_version: 2.5.13
---

A Map component that uses Apple Maps or Google Maps on iOS and Google Maps on Android.

For non-crna Vue-Native projects, use the `react-native-maps` and link them.

For Vue-Native projects created with Crna, mapView from `expo` can be diretly used as shown below :

```html
<template>
  <view  :style="{ flex: 1 }">
    <mapView
        :style="{ flex: 1 }"
        :initialRegion="{
            latitude: 37.78825,
            longitude: -122.4324,
            latitudeDelta: 0.0922,
            longitudeDelta: 0.0421,
        }"
      />
  </view>
</template>

<script>
import { MapView } from "expo";
export default {
   components: {
    MapView
  }
};
</script>
```
