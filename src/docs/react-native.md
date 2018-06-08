---
title: React Native
type: guide
order: 9
vue_version: 2.5.13
gz_size: "30.67"
---

Vue Native transpiles to React Native. React Native is a framework to build native Android and iOS apps using JavaScript.

*So, you can one-to-one map Vue Native components to React Native components.*

What changes in Vue Native (when compared to React Native)?
• You write .vue files instead of .js
• Any .vue file has three parts which are `<template />, <style /> and <script />`
• With `template` and `style` section we use hyphen-case and Pascal case in the script section. This includes the name of the component, style properties and style names

Vue Native is like a syntactic sugar for React Native. We can import any React Native component as it is and start using it

## Relation to Custom Elements

You may have noticed that Vue Native components are very similar to [**React Native Components**](https://facebook.github.io/react-native/docs/getting-started.html). You can use All React Native Component, by making use of the `kebab case (hyphen-delimited)` equivalent components. This is because Vue Native is a wrapper around the React Native APIs.