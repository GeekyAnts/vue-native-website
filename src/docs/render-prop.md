---
title: Component As Prop
type: guide
order: 11
vue_version: 2.5.13
gz_size: "30.67"
---

The `render prop` API eliminates the need to use JSX. There are mainly two attributes used here based on whether it needs a function or a component.

## render-prop-fn

If the component used expects a `callback` , `render-prop-fn` can be used.
Take this example of a `flat-list` where the `renderItem` provides a `callback` and expects a component to be returned.

```html
<flat-list
  :style="{backgroundColor: 'red', height: 200, width: 200, overflow: 'hidden'}"
  :data="[{key: 'a'}, {key: 'b'}]" >
  <view render-prop-fn="renderItem" >
    <text>{{args.item.key}}</text>
  </view>
</flat-list>
```

The `render-prop-fn` can be provided directly to the component to be rendered as shown above. The component that specify `renderItem` along with it's children are mapped to the `renderItem` attribute of the `flat-list`.

By default `args` provides the `item` that is provided by callback and can be used as shown.
If you want to specify multiple arguments you can declare `arguments='arg1,arg2'` along with `render-prop-fn`.

```html
    <view render-prop-fn="renderItem" arguments="arg1,arg2">
        <text>{{arg1.item.key}}</text>
    </view>
```

## render-prop

`render-prop` is similar to `render-prop-fn` that eliminates the use of JSX but used when the prop expects a component instead of callback. When an attribute in the component expects a component, like in the `flat-list`'s `ListFooterComponent`, we make use of `render-prop` .

```html
<flat-list
  :style="{backgroundColor: 'red', height: 200, width: 200, overflow: 'hidden'}"
  :data="[{key: 'a'}, {key: 'b'}]" >
  <view render-prop-fn="renderItem" >
    <text>{{args.item.key}}</text>
  </view>
  <view
    render-prop="ListFooterComponent"
    :style="{
      paddingVertical: 20,
      borderTopWidth: 1,
      borderColor: '#CED0CE'}">
    <activity-indicator animating size="large" />
  </view>
</flat-list>
```

The component that specify the `ListFooterComponent` along with it's children are mapped to the `flat-list`'s `ListFooterComponent` attribute.
In the above example we have used both `render-prop-fn` and `render-prop`. Similarly you can define multiple children with any of the above API's but must be supported by the parent component.
