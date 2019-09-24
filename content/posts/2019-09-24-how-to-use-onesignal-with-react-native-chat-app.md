---
template: post
title: How to use OneSignal with React Native Chat App
slug: How-to-use-OneSignal-with-React-Native-Chat-App
draft: true
date: 2019-09-24T03:43:34.835Z
description: >-
  In this tutorial, we are going to learn how to integrate OneSignal
  pushnotification to React Native Chat app project. For this tutorial, we are
  onlygoing to implement it in the Android platform using an android device.
  OneSignal
category: react native
tags:
  - react native
  - onesignal
---
![](https://imgur.com/jli1HpK.png)

In this tutorial, we are going to learn how to integrate OneSignal push
notification to React Native Chat app project. For this tutorial, we are only
going to implement it in the Android platform using an android device. OneSignal
is a popular service that enables push notifications on a device, abstracting
details such as the platform the device is running on. By using OneSignal
plugin, mobile applications can send and receive push notifications. So, we are
going to implement this OneSignal service to our React Native chat app in order
to enable push notifications.
### Pre-requirement

Basically, to integrate OneSignal to React Native, We must have the following
two requirements:

1.  [a starter code](https://github.com/krissnawat/pubnub-react-native-chat/tree/add_auth0)
1.  Android hardware device (Because android emulator is too slow)

### Setting up OneSignal

In the first step, we are going to set up our OneSignal service. For this, we
need to sign in to [Onesignal](https://app.onesignal.com/login) website then
login to our OneSignal account. Note that: If you don’t have an account you can
easily make one by registering to their site or by using Google, Facebook or
Github login as shown in the screenshot below:

![](https://cdn-images-1.medium.com/max/800/1*StdR5iPnAEQrfMo8zIdjLw.png)

After the login, we need to create a new app. For that, first, we need to select
a platform. Here, we are going to select “Google Android” platform as shown in
the code snippet below:

![](https://cdn-images-1.medium.com/max/800/1*Cl5mVqfKpmoczSayu_uBkg.png)

Then, we need firebase server key to establish communication between OneSignal
and Firebase cloud messaging as shown in the screenshot below:

![](https://cdn-images-1.medium.com/max/800/1*ZYz7cMcB5R8kYEPL_crCNw.png)

For the Firebase server key, we need to go to the Firebase console and create a
firebase app. After, the successful creation of Firebase app we need to go to
“Settings”. Then, we need to navigate to “cloud messaging” tab and copy **server
key** and **sender id **as shown in the screenshot below:

![](https://cdn-images-1.medium.com/max/800/1*EvqwqzSHIO7kqDlIqGA2-w.png)

Now, we need to return to our OneSignal platform configuration and paste both
Firebase **Server key **and **Sender ID** to OneSignal form as shown in the
screenshot below:

![](https://cdn-images-1.medium.com/max/800/1*zyeZ7_N3rrWfWEj7yoygkg.png)

After the completion of the platform configuration, We need to choose SDK for
our OneSignal app. Here, we are going to select **React native SDK **as our apps
SDK.

![](https://cdn-images-1.medium.com/max/800/1*mxvRr-Vh4WMApK8aqTrJVA.png)

After the selection of SDK, we get our AppID for sending push notification as
shown in the screenshot below:

![](https://cdn-images-1.medium.com/max/800/1*vHdeHn2lU7qtcIJJIZ2Fzw.png)

Now, we need to click on “DONE” button which lets us navigate to our OneSignal
dashboard as shown in the screenshot below:

![](https://cdn-images-1.medium.com/max/800/1*nomIT_CW5l3gSonEnuQKdQ.png)

After this, we need to go to our React native SDK
[document](https://documentation.onesignal.com/docs/react-native-sdk-setup) and
add OneSignal code snippet code to our app which is shown in the code snippet
below:

```javascript
  constructor(props) {
    super(props);
    ................
    OneSignal.init(process.env.onesignal_key);
    OneSignal.addEventListener("received", this.onReceived);
    OneSignal.addEventListener("opened", this.onOpened);
    OneSignal.addEventListener("ids", this.onIds);
    OneSignal.configure();
    ................
  }

 onReceived = notification => {
    console.log("Notification received: ", notification);
  };

  onOpened = openResult => {
    console.log("Message: ", openResult.notification.payload.body);
    console.log("Data: ", openResult.notification.payload.additionalData);
    console.log("isActive: ", openResult.notification.isAppInFocus);
    console.log("openResult: ", openResult);
  };

  onIds = device => {
    console.log("Device info: ", device);
    this.setState({ device });
  };
```

Here, We use three functions to display the activity log as you can see in the
code snippet above. And when we open the app, it will automatically register to
OneSignal as shown in the screenshot below:

![](https://cdn-images-1.medium.com/max/800/1*VBSlGlJYVa-v58TZuqwJjA.png)

Now, let’s test our OneSignal app by sending send a message from the OneSignal
console.

First, we need to go to the **Message **tab then\*\* \*\*create a new message as
shown in the OneSignal console screenshot below:

![](https://cdn-images-1.medium.com/max/800/1*CuI6kS1Jb3jvNzKEOkoutw.png)

We can see the setting up of our first message in the screenshot below to the
left and how a push notification will appear in the screenshot displayed below
to the right:

![](https://cdn-images-1.medium.com/max/800/1*EJ6yWabCMpiNiIVyZfPWQw.png)

Now, we need to confirm if we are really sending a message to the Android
device. If we are sending a message then we click on **SEND MESSAGE** button as
shown in the screenshot below:

![](https://cdn-images-1.medium.com/max/800/1*aDnWYBjwKMsNg4BC2_6Qvg.png)

<br>

Here, we can see that it’s working as expected. We can receive a message in our
Android device as you can see in the simulation below:

![](https://cdn-images-1.medium.com/max/1200/1*4V62wx2OqHnfpKOnqte8rA.gif)

After this, we are going to redirect our to message analytic dashboard which is
shown in the screenshot below:

![](https://cdn-images-1.medium.com/max/800/1*mD5OK_RdGR8pk0cZlM7emQ.png)

<br>
<a href="https://www.instamobile.io/app-templates/react-native-chat-app-template?ref=4094" target="_blank">
<img src="/Social Chat App Template.png">
</a>

### Sending Push Notification

In this step, we are sending a push notification to our React Native chat app
using the OneSignal app that we configured in our previous step. Here, we are
going to use [rest
API](https://documentation.onesignal.com/reference#section-example-code-create-notification)
to send message to OneSignal server. We need to construct a URL and a payload as
shown in the code snippet below:

```javascript
sendNotification = data => {
  let headers = {
    "Content-Type": "application/json; charset=utf-8",
    Authorization: "Basic 'OneSignal Server Key'"
  };

  let endpoint = "https://onesignal.com/api/v1/notifications";

  let params = {
    method: "POST",
    headers: headers,
    body: JSON.stringify({
      app_id: "xxxxxxxx-xxxxxx-xxx-a14a-xxxxxx",
      included_segments: ["All"],
      contents: { en: data }
    })
  };
  fetch(endpoint, params).then(res => console.log(res));
};
```

Here, we can just copy the code above and paste it to our React Native project
but we must remember that we need a server key for creating Authorization header
and app_id to construct the message.

Note that: More message configurations are available in the documentation of
OneSignal
[here](https://documentation.onesignal.com/reference#create-notification).

Now, we need to add a _sendNotification()_ function with a message to the
*componentDidMount *of our React Native app as shown in the code snippet below:

```javascript
    componentDidMount() {
       this.sendNotification('Greeting from Chat App');
    }
```

Now, we can observe that notification is displayed like an alert box when we
launch our app as shown in the device screenshot below:

![](https://cdn-images-1.medium.com/max/800/1*5Vt9ahf_rpF27qwIsKoSuA.png)
<span class="figcaption_hack">\</span>

Now, we need to use this feature when a user joins or a user leaves the
channel. For this, we can use the code provided in the code snippet below with
the _PresenceStatus_ function:

```javascript
  PresenceStatus = () => {
    this.pubnub.getPresence(RoomName, presence => {
      if (presence.action === "join") {
        let users = this.state.onlineUsers;

        users.push({
          state: presence.state,
          uuid: presence.uuid
        });

        this.setState({
          onlineUsers: users,
          onlineUsersCount: this.state.onlineUsersCount + 1
        });
        this.props.navigation.setParams({
          onlineUsersCount: this.state.onlineUsersCount
        });
        this.sendNotification(presence.uuid + " join room");
      }

      if (presence.action === "leave" || presence.action === "timeout") {
        let leftUsers = this.state.onlineUsers.filter(
          users => users.uuid !== presence.uuid
        );

        this.setState({
          onlineUsers: leftUsers
        });
        console.log("leave room");
        const length = this.state.onlineUsers.length;
        this.setState({
          onlineUsersCount: length
        });
        this.props.navigation.setParams({
          onlineUsersCount: this.state.onlineUsersCount
        });
        this.sendNotification(presence.uuid + " leave room");
      }
```

Here, we are calling _sendNotification()_ in two conditions. One is when a user
enters the channel and other is when a user leaves the channel as shown in the
code snippet above. Now, let's try it out in our android device.

For testing mode, we can use Android emulator on Mac. But, it is very slow so we
stream a hardware device and use iPhone simulator as shown in the code snippet
below:

![](https://cdn-images-1.medium.com/max/800/1*WUSilhgDBeCAphcCp2eRfw.gif)

We can see that it’s working properly. But the notification does not appear
familiar and integrated well in the UI. So, for that, we need to the
notification alert from the header. The solution to config notification style in
the OneSignal documentation and also available in the code snippet shown below:

Now, we need to reload our React app and check it out. You can see that
everything working as it should now. This completes our interesting tutorial for
integrating a push notification using OneSignal service into our react native
chat application.

![](https://cdn-images-1.medium.com/max/800/1*4q92EGp07P-uS8d1V29m0g.gif)

### Conclusion

In this tutorial, we learned how to configure OneSignal service by creating a
OneSignal app. Then, by using the OneSignal app we learned how to enable push
notification in our React Native chat app. We also got detail insight on how to
send a push notification when a user joins or leaves a chat room. The code for
this tutorial is freely available on
[Github](https://github.com/krissnawat/pubnub-react-native-chat/tree/add-push-notification-with-OneSignal).

<p>
This site contains affiliate links to products. We may receive a commission for purchases made through these links.
</p>
