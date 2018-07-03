---
title: Lottie
type: guide
order: 19
vue_version: 2.5.13
gz_size: "30.67"
---

## Lottie

[Lottie](https://airbnb.design/lottie) is the animation library from AirBnB and Expo has the default support it.

```html
<view class="container">
    <lottie
      ref="lottieAnimation"
      :style="{
        width: 400,
        height: 400,
        backgroundColor: '#eee',
      }"
      :source="animation ? animation  : {}"
    />
    <view class="button-container">
        <button title="Start Animation" :onPress="playAnimation" />
    </view>
</view>
```

```JS
<script>
import lottieAnimationJson from "./lottieAnimation.json";
import { DangerZone } from "expo";
const { Lottie } = DangerZone;

export default {
  components: { Lottie },
  data: function() {
    return {
      animation: null
    };
  },
  methods: {
    async loadAnimationAsync() {
      try {
        const lottieAnimationJsonResponse = await fetch(
          "https://cdn.rawgit.com/airbnb/lottie-react-native/635163550b9689529bfffb77e489e4174516f1c0/example/animations/Watermelon.json"
        );
        const parsedJson = await lottieAnimationJsonResponse.json();
        this.animation = parsedJson;

        this.playAnimation();
      } catch (error) {
        console.log(
          "%c some inside loadAnimationAsync ",
          "background: salmon; color: black",
          error
        );
      }
    },
    playAnimation() {
      if (!this.animation) {
        this.loadAnimationAsync();
      } else if (this.$refs.lottieAnimation) {
        this.$refs.lottieAnimation.reset();
        this.$refs.lottieAnimation.play();
      }
    }
  },
  mounted() {
    this.playAnimation();
  },
  beforeUpdate() {
    this.playAnimation();
  }
};
</script>
```

```css
<style>
.container {
  background-color: #fff;
  align-items: center;
  justify-content: center;
  flex: 1;
}
.button-container {
  padding-top: 20;
}
</style>
```

<div class="hello-world-container">
  <div class="hello-world-wrapper">
    <img src="/images/lottie.gif" class="img-wrapper" />
  </div>
</div>
