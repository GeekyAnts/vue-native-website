---
title: Conditionals and Loops
type: guide
order: 6
vue_version: 2.5.13
gz_size: "30.67"
---
## v-if
> Conditionally renders the element or View.

It's easy to toggle the presence of an element, too! Go ahead and click the button and watch what happens. In Vue, not only can we call methods from event handlers, but we can also run single evaluation statements inline, directly inside the handler. 

This is very handy when it comes to something like the `v-if` example, you can simply toggle the boolean in our data property inline, instead of having to write a seperate method, then call that method when the event gets fired.

```html
<view>
  <text v-if="seen">Now you see me</text>
  <button :on-press="seen = !seen>Click to Toggle</button>
</view>
```

```JS
<script>
export default {
  data: function() {
    return {
      seen: false
    };
  }
};
</script>
```

## v-else
> Conditionally renders the else block of a `v-if` directive.
The `v-else` directive is a secondary(optional) directive that gets used with `v-if`. Much like the way an if/else conditional statement works in Javascript, this works similarly in rendering an element, `else` redering a different element, based on the value of a data property on our Vue Instance.

Notice how `v-else` doesn't have a parameter input on it? Thats because `v-else` is implicit to the most previous `v-if` directive in use. Else is will default to an error of missing 'v-if directive'

```html
<view>
  <text v-if="seen">Now you see the first one.</text>
  <text v-else>Now you see the second one.</text>
  <button :on-press="seen = !seen>Click to Toggle</button>
</view>
```

```JS
<script>
export default {
  data: function() {
    return {
      seen: false
    };
  }
};
</script>
```

## v-show
> Conditionally display an element or View
Much like the v-if directive, v-show acts in a similar way being that they both change the display of the target element or View, but with one key difference.

That difference is how the directive achieves this. `v-if` will remove the element from the view completely, where as `v-show` keeps the element on the View, and only adjusts the opacity to 0%, or transparent.
```html
<view>
  <text v-if="seen">Now you see me</text>
  <button :on-press="seen = !seen>Click to Toggle</button>
</view>
```

```JS
<script>
export default {
  data: function() {
    return {
      seen: false
    };
  }
};
</script>
```


## v-for
> Renders a list of items using the data from an Array
This example demonstrates that we can bind data, and dynamically render the UI elements to the View based on the values inside the Array we are looping through. V-for is basically a ForEach loop.

```html
<view class="container">
  <text class="text-container" v-for="todo in todos" :key="todo.text">
    {{ todo.text }}
  </text>
</view>
```

```JS
<script>
export default {
  data: function() {
    return {
      todos: [
        { text: "Learn JavaScript" },
        { text: "Learn Vue" },
        { text: "Build something awesome" }
      ]
    };
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
.text-container {
  color: blue;
  padding: 2;
}
</style>
```

<div class="hello-world-container">
  <div class="hello-world-wrapper">
    <img src="/images/vFor_text_list.png" class="img-wrapper" />
  </div>
</div>
