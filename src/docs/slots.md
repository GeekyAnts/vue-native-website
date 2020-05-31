---
title: Slots
type: guide
order: 10
vue_version: 2.5.13
gz_size: "30.67"
---

> Note : Slots are supported only with vue-native-helper version 0.0.9 and above.

## Slot Content

Vue Native just like Vue implements a content distribution API that’s modeled after the current Web Components spec draft, using the `<slot>` element to serve as distribution outlets for content.

In order to allow a parent component to pass elements into a child component, provide a `<slot></slot>` element inside the child component. Now, using the `child` component in the parent, any code in the parent's `<child>` component will replace `<slot/>` in the child component.

This allows you to compose parent and child elements as shown :

```html
//parent element
<template>
  <view>
    <child>
      <text>Will render myself in the child component. You are welcome.</text>
    </child>
  </view>
</template>
```

```html
//child component
<template>
  <view>
    <slot></slot>
  </view>
</template>
```

If you run this, when the component renders, the `<slot>` element will be replaced by `<text>Will render myself in the child component. You are welcome.</text>`. Slots can contain any template code or even other components.

If `child` did not contain a `<slot>` element, any content passed to it would simply be discarded.

## Named Slots

There are times when it’s convineint to have multiple slots.

Consider this parent element :

```html
<template>
  <view class="container">
     <child>
       <text slot="top">Top text</text>
       <text slot="bottom">Bottom text</text>
       <text>Text with no name</text>
       <text slot="middle">Middle text</text>
     </child>
  </view>
</template>
```

Specify the slot names in the attribute `slot`.

The `<slot>` element in the child component has a special attribute, `name`, which can be used to define named slots.

```html
<template>
  <view>
    <slot name="bottom"></slot>
    <slot name="middle"></slot>
    <slot name="top"></slot>
    <slot></slot>
  </view>
</template>
```

When the component renders, it will be in this order :

```
Bottom text
Middle text
Top text
Text with no name
```

Notice that the order of the texts rendered corresponds to the `slots` arranged in the child component. The unnamed slot acts as the default slot.

## Scoped Slots

Sometimes you’ll want to provide a component with a reusable slot that can access data from the child component. For example, when building a simple `<todo-list>` component, in some parts of the app, you may want the individual todo items to render something different than just what was defined in the `<todo-list>`. This is where scoped slots come in.

To understand this better let's take a simple example, consider two components named `parent` and `child`, conveniently named to explain this better.

Both these components look like this:

```html
//Parent component
<template>
  <view class="container">
    <child>
      <text>Parent data</text>
      <template scope="slotProps">
        <text>{{ slotProps.texts.text }}</text>
      </template>
    </child>  
  </view>
</template>
```

A `scope` attribute can be used to receive the props for the slot from the child component. The data from the child element can be accessed as shown above with `slotProps.texts.text`.

```html
//Child component
<template>
  <view class="container">
    <slot v-bind:texts="texts">
      {{ texts.text }}
    </slot>
  </view>
</template>
```

The `slot` component is used in the child element and is bound through the `v-bind` to its data. The data that is bound here can be used in the parent component as shown.

The two texts will be rendered in this manner :

```
Parent data
Child component data
```
