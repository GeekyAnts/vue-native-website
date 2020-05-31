---
title: Device APIs
type: guide
order: 12
vue_version: 2.5.13
gz_size: "30.67"
---

Some of the functionalities that an app needs that depends on the hardware of the device such as `accelerometer`, `location`, `camera`, `push notifications` among many others may be accessed and used as shown in this documentation.

For non-crna projects created with vue-native, you may use packages such as `react-native-sensors` and link them to get started.

## Accelerometer

With Expo, you need to import the `Accelerometer` module from `expo-sensors`.

Install the package using:
```shell
npm i expo-sensors
```

and import it as follows:
```js
import { Accelerometer } from "expo-sensors";
```

Let's initialize our `accelerometerData` and bind it to our `template`.

```js
data() {
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

Refer the expo [documentation](https://docs.expo.io/versions/latest/sdk/accelerometer) for more details.

## Geolocation
```shell
npm i expo-location expo-permissions
```

Accessing the device's hardware to get to know it's location can be acheived by using APIs provided by `expo`.

You must request permission to access the user's location before attempting to get it. To do this, you will want to use the Permissions API. You can see this in practice in the following example.

If you deny the application permission to access location, it will continue to block. To overcome this on iOS, you can use the device's Expo application setting to "allow while using" or you can delete and re-install Expo app.

```html
<template>
  <view class="container">
    <touchable-opacity :on-press="getLocation">
      <text class="text-field-title">Get Location</text>
    </touchable-opacity>
    <text class="text-field-title">Location Object:</text>
    <text>{{ location }}</text>
    <text class="text-field-title">Latitude Only:</text>
    <text>{{ latitude }}</text>

    <text class="text-error">{{ errorMessage }}</text>
  </view>
</template>
```

```html
<script>
import * as Location from "expo-location";
import * as Permissions from "expo-permissions";

export default {
  data: function() {
    return {
      location: {},
      latitude: "",
      errorMessage: ""
    };
  },
  methods: {
    getLocation: function() {
      Permissions.askAsync(Permissions.LOCATION)
        .then(status => {
          if (!status.granted) {
            this.errorMessage = "Permission to access location was denied";
          } else if (status.granted) {
            Location.getCurrentPositionAsync({}).then(location => {
              this.location = location;
              this.latitude = location.coords.latitude
              this.errorMessage = "";
            });
          }
        })
        .catch(err => {
          console.log(err);
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

## Camera

For vue-native projects created with CRNA, we will be using `expo`'s `camera` component.

With use of Camera one can also take photos and record videos that are saved to the app's cache. Morever, the component is also capable of detecting faces and bar codes appearing on the preview.

Requires `Permissions.CAMERA`. Video recording requires `Permissions.AUDIO_RECORDING`.

```shell
npm i expo-camera 
```

### Basic Example


```html
<template>
  <view class="container">
    <camera class="container" :type="this.type"/>
  </view>
</template>
```

```html
<script>
import * as Permissions from 'expo-permissions';
import { Camera } from 'expo-camera';


export default {
 data: function() {
   return {
     hasCameraPermission: false,
     type: Camera.Constants.Type.back,
   };
 },
 mounted: function() {
   Permissions.askAsync(Permissions.CAMERA)
     .then(status => {
       hasCameraPermission = status.status == "granted" ? true : false;
     }).catch((err)=>{
        console.log(err);
     });
 },
 components: { Camera },
};
</script>
```

```css
<style>
.container {
  flex: 1;
}
.text-color-primary {
  color: blue;
}
</style>
```

## Push Notifications

Push notifications at their core are simply a way of alerting users to information that they have opted-in to from apps and services. They also help the apps deliver timely and relevant information to users, and in doing so, staying top of users' mind.

We will be looking into how we can send push notifications using `expo` since we are going to use `vue-native` projects created using `crna`.

In order to use `vue-native` projects created using `react-native` cli, libraries such as `react-native-push-notification` can be used.

There are three main steps to wiring up push notifications when using `expo`:
• Sending a user's Expo Push Token to your server.
• Calling Expo's Push API with the token when you want to send a notification.
• Responding to receiving and/or selecting the notification in your app (for example to jump to a particular screen that the notification refers to).

To make this more simpler to get started, we won't be using a server to store the token and send notifications to the device, rather we will be using the [Expo push notification tool](https://expo.io/dashboard/notifications) to test push notifications.

### Register device with `Expo` and store the token.

In order to send a push notification to somebody, we need to know about their device. Let's look at the function that is used to register the device.

```js
registerForPushNotifications: async function() {
  const { status: existingStatus } = await Permissions.getAsync(
    Permissions.NOTIFICATIONS
  );
  let finalStatus = existingStatus;

  // only ask if permissions have not already been determined, because
  // iOS won't necessarily prompt the user a second time.
  if (existingStatus !== "granted") {
    // Android remote notification permissions are granted during the app
    // install, so this will only ask on iOS
    const { status } = await Permissions.askAsync(
      Permissions.NOTIFICATIONS
    );
    finalStatus = status;
  }

  // Stop here if the user did not grant permissions
  if (finalStatus !== "granted") {
    return;
  }

  // Get the token that uniquely identifies this device
  Notifications.getExpoPushTokenAsync().then(token => {
    console.log(token);
  });
}
```

We are logging our `token` so that we can use it in the `Expo push notification tool` to send the test notifications to device.

### Call Expo's Push API with the user's token

Push notifications have to come from somewhere, and that somewhere is your server, but for our learning here, let's use the [Expo push notification tool](https://expo.io/dashboard/notifications) and add the required fields.

Once sent, the notification appears as shown below.

<div class="hello-world-container">
  <div class="hello-world-wrapper">
    <img src="./../images/push-notification.gif" class="img-wrapper" />
  </div>
</div>

### Handle receiving and/or selecting the notification

For Android, this step is entirely optional -- if your notifications are purely informational and you have no desire to handle them when they are received or selected, you're already done.

Handling push notifications is quite straightforward with Expo, all you need to do is add a listener to the Notifications object.

Let's bind a variable from the data section that we can change when user clicks on the notification.

```html
<template>
  <view class="container">
    <text class="text-color-primary">{{JSON.stringify(notification.data)}}</text>
    </view>
</template>
```

```js
data() {
  return {
    notification: {}
  };
},
```

Also a function that handles the notification and also attach a listener so this function is called when the notification is to be handled.

```js
 created: function() {
    this.registerForPushNotificationsAsync();
    this._notificationSubscription = Notifications.addListener(
      this._handleNotification
    );
  },

  methods:{
    _handleNotification: function(notification) {
      this.notification = notification;
    },
  }
```
