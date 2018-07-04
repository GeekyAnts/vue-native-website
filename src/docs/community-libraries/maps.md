---
title: Maps
# type: guide
# order: 16
type: community-libraries
order: 2
vue_version: 2.5.13
gz_size: "30.67"
---

A Map component that uses Apple Maps or Google Maps on iOS and Google Maps on Android.

For non-crna Vue-Native projects, use the `react-native-maps` and link them.

For Vue-Native projects created with Crna, mapView from `expo` can be diretly used as shown below :

```html
<template>
  <view  class="container">
    <map-view class="container"
        :initial-region="coordinates"
      />
  </view>
</template>

<script>
import { MapView } from "expo";
export default {
    data: function() {
    return {
      coordinates: {
        latitude: 12.91074,
        longitude: 77.5996363,
        latitudeDelta: 0.0922,
        longitudeDelta: 0.0421
      }
    };
  },
   components: {
    MapView
  }
};
</script>
<style>
.container {
  flex: 1;
}
</style>
```
