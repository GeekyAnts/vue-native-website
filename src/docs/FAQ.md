---
title: FAQ
type: guide
order: 20
vue_version: 2.5.13
gz_size: "30.67"
---

## Frequently Asked Questions

### What are the advantages/differences of Vue Native over React Native

Vue Native is layer based on top of React Native. The template definition is based on Vuejs which is then converted into suitable react native code. With this, we are able to take advantage of the existing react native ecosystem where a lot of third party libraries and support are available.

### Can I reuse vuejs web app code?

No. You cannot, since vue-native does not make use of html tags. It's not possible to reuse the vuejs web app code.

### Support for $emit for communication from child to parent

There's a workaround for this issue. https://github.com/GeekyAnts/vue-native-core/issues/25#issuecomment-412457861.

### What about third party libraries for vue-native

All the react-native libraries are supported by vue-native. You can look into [third party libraries section](./community-libraries-doc.html) for some of the examples.
