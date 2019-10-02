---
template: post
title: 'AirBnB Clone with React Native Part 5: Loading Modal Implementation'
slug: airbnb-clone-with-react-native-part-5-loading-modal-implementation-2cdl
draft: false
date: 2019-10-02T03:52:10.419Z
description: >
  In part 5, we’re going to continue from where we left off by implementing a
  loading modal before generating the error notification message. Usually, we
  might notice a delay in the response from the server when we initialize the
  request. This may be caused by a slow internet connection or slow device.
category: react native
tags:
  - react native
---


This tutorial is the fifth chapter of our implementation of an <a href="https://www.instamobile.io/app-templates/real-estate-app-template-react-native/?ref=4094&amp;campaign=hackernoon" title="https://www.instamobile.io/app-templates/real-estate-app-template-react-native/?ref=4094&amp;campaign=hackernoon" target="_blank" >AirBnB clone in React Native</a>. In the previous chapter, we successfully implemented a login error notification system. In case you need to get caught up, here are links to [parts 1–4](https://heartbeat.fritz.ai/@kris101?source=post_page-----8a399154ac02---------------------- "https://heartbeat.fritz.ai/@kris101?source=post\_page-----8a399154ac02----------------------")

In part 5, we’re going to continue from where we left off by implementing a loading modal before generating the error notification message. Usually, we might notice a delay in the response from the server when we initialize the request. This may be caused by a slow internet connection or slow device.

Here, we’re going to create or simulate such a scenario while logging in. In summary, we’re going to create a loading modal that executes when we press the login button to simulate the delay in response and show the notification error message that we implemented in the previous chapter after loading completes.

**_So let’s get started!_**

**Creating a Loader Component**

First, we’re going to create a simple component named Loader in the Loader.js file. Here, we need to create a simple class named Loader that extends to the Component module of React.

We’re going to implement a loading modal in this Loader component, so we need to import the Modal component from the **react-native** package. For now, we’re just going to render text using a Text component wrapped inside the Modal component, as shown in the code snippet below:

```
import React, { Component } from 'react';
import { View, Image, Modal, StyleSheet, Text} from 'react-native';

export default class Loader extends Component {
  render() {
    return (
      <Modal visible={true}>
          <Text>This is modal</Text>
      </Modal>
    );
  }
}
```

Next, we’re going to import our Loader component into our Login component in the Login.js file:

```
import Loader from “../components/Loader”;
```

Then, we need to initialize or render our Loader component below the Notification component:

```
<View>
  <Notification
    showNotification={showNotification}
    handleCloseNotification={this.handleCloseNotification}
    title="Error"
    message={this.state.error} />
</View>
<Loader />
```

As a result, we’ll get the modal in the Loader component with text displayed at the top of the screen, as shown in the emulator screenshot below:

 ![](https://cdn.filestackcontent.com/zcf6cx6QQqWotvyjZqra)

> Looking for new ways to elevate your mobile app’s user experience? [With Fritz AI, you can teach your apps to see, hear, sense, and think. Learn how and start building with a free account.](https://www.fritz.ai/product/standard.html?utm_campaign=buildapps9&utm_source=heartbeat "https://www.fritz.ai/product/standard.html?utm\_campaign=buildapps9&utm\_source=heartbeat")

## Configuring and styling modal

Next, we’re going to configure the modal using props so that it will look more appealing. The props we’re going to use here are animationType, transparent, and visible. The animationType and visible props are defined in the initialized Loader component in the Login.js file, as shown in the code snippet below:

```
<Loader 
  modalVisible = {true}
  animationType="fade"  
/>
```

The code in the above snippet sends the modalVisible and animationType props from parent component—i.e. the Login component—to the child component—i.e. the Loader component.

Now, we need to receive the props into the child Loader component and configure the modal accordingly. The modalVisible and animationType props are made mandatory in the Loader component. The code to receive the props and configure the modal is provided below:

```
import { PropTypes } from 'prop-types';
export default class Loader extends Component {
  render() {
    const { animationType, modalVisible } = this.props;
    return (
      <Modal animationType={animationType} transparent={true} visible={modalVisible}>
          <View style={styles.wrapper}>
            <Text>This is modal</Text>
          </View>
      </Modal>
    );
  }
}

Loader.propTypes = {
  animationType: PropTypes.string.isRequired,
  modalVisible: PropTypes.bool.isRequired,
};
```

As we can see above, the props are received and then bound to required modal props. Configuring the modal isn’t enough so we need to style the modal View wrapper as well. The styling is done using the Stylesheet component, and the styles required are provided in the code snippet below:

```
wrapper: {
  zIndex: 9,
  backgroundColor: 'rgba(0,0,0,0.6)',
  position: 'absolute',
  width: '100%',
  height: '100%',
  top: 0,
  left: 0,
},
```

Now, our resulting modal will appear as shown in the following screenshot:

 ![](https://cdn.filestackcontent.com/1BP5olJ3QyiKqURJudhJ)

**Adding a GIF loading file to Image component in Modal**

In this step, we’re going to add a GIF file, which has a loading image in place of the Text component inside the Modal component of our Loader.js file. For that, we need to import the Image component from the react-native package, which we’ve already done at the beginning.

Then, in the source prop of the Image component, we need to add a location to our GIF file. The location is (‘../img/greenLoader.gif’). The code to add this is provided below:

```
loaderContainer: {
    width: 90,
    height: 90,
    backgroundColor: colors.white,
    borderRadius: 15,
    position: 'absolute',
    left: '50%',
    top: '50%',
    marginLeft: -45,
    marginTop: -45,
  },
```

As we can see in the above code snippet, the Image component is wrapped by another View component. Both the components are styled using Stylesheet. The styling for the components is provided in the code snippet below:

 ![](https://cdn.filestackcontent.com/6lNHAGdTn2J5l4Gz8vSS)

Now, let’s have the look at our resulting loading modal:

As we can see, the loading GIF image appears at the center of the modal. Now, we need to execute this loading modal when the login button is pressed.

> The next revolution in mobile development? Machine learning. Don’t miss out on the latest from this emerging intersection. [Sign up for weekly updates from our crew of mobile devs and machine learners.](https://www.fritz.ai/newsletter?utm_campaign=heartbeat-newsletter-fomo2&utm_source=heartbeat "https://www.fritz.ai/newsletter?utm\_campaign=heartbeat-newsletter-fomo2&utm\_source=heartbeat")

Handling Loading Modal Visibility **Showing Loading Modal when Login is pressed**

In this step, we’re going to execute the loading modal when we press the login button. For this, we need to set a state variable in the Login.js file that handles the execution of the loading modal.

Here, we set the state variable as loadingVisible, which takes a boolean value. If the loadingVisible state is true, the loading modal appears on the screen, and if it’s set to false , the loading modal doesn’t appear on the screen. The code snippet to initialize the state variable loadingVisible is given below:

```

this.state = {
  user: null,
  email: "",
  password: "",
  formValid: true,
  error: "",
  loadingVisible: false
};
```

Now we need to initialize the loadingVisible state inside the render() function so that it’s easily accessible to the render elements. The code to do this is provided below:

```
render() {
  const { formValid, loadingVisible } = this.state;
  const showNotification = formValid ? false : true;
```

Now we need to pass the loadingVisible state as a prop to the Loader component by binding it to modalVisible prop, as shown in the code snippet below:

```
<Loader 
  modalVisible = {loadingVisible}
  animationType="fade"  
/>
```

Finally, we need to handle the change of the loadingVisible state when the login button is pressed. We know that when we press the login button on the screen, it executes the Login() function of the Login.js file. So we need to change the state of loadingVisible while executing the Login() function, as shown in the code snippet below:

```
Login = () => {
    this.setState({ loadingVisible: true });

    firebase
      .auth()
      .signInWithEmailAndPassword(this.state.email, this.state.password)
      .then(user => {
        this.setState({ user });
      })
      .catch(error =>
        this.setState({
          error: error.message,
          formValid: false
        })
      );
  };
```

Now when we press the login button, the Login() function executes, changing the loadingVisible state to true. As a result, the loading modal becomes visible on the screen:

 ![](https://cdn.filestackcontent.com/C4m2f0LSkyep9ZyRXDTJ)

As we can see in the simulation above, the loading modal appears when we press the login button.

But the loading modal needs to disappear when the error notification message pops up at the bottom.

**Hiding Loading Modal when the Notification is displayed**

Here, we’re going to hide the loading modal when the error notification component pops up. It’s very simple. We just need to set the loadingVisible state to false while sending the error message prop to the Notification component in the Login() function of the Login.js file. The code to do this is provided in the code snippet below:

```
Login = () => {
    this.setState({ loadingVisible: true });

    firebase
      .auth()
      .signInWithEmailAndPassword(this.state.email, this.state.password)
      .then(user => {
        this.setState({ user });
        this.setState({ loadingVisible: false });
      })
      .catch(error =>
        this.setState({
          error: error.message,
          formValid: false
          loadingVisible: false
        })
      );
  };
```

Now, let’s refresh the emulator and check to see if everything works:

 ![](https://cdn.filestackcontent.com/6fGkz7e6REGQvMYBSYNF)

As we can see, the loading modal disappears when the notification message pops up.

This successfully completes our tutorial for implementing the Loading modal in our AirBnB clone using React Native.

## Conclusion

In this tutorial, we learned how to implement a Loading modal to simulate a delay in the response from the server.

We also learned how to pass data between parent and child components as props in React Native. We got detailed insight on how to use the Modal component and how to configure it using the props. To this end, we successfully created a loader which appears when logging in and disappears when an error notification pops up. This is a perfect example to simulate a loader while we wait for the response from the server. Lastly, we learned how to control the styles dynamically with the state variable and how to add animations.

All the code for this tutorial is available in this [GitHub repo](https://github.com/krissnawat/airbnbclone-with-react-native/commit/b54a6e64bc8ce81981d24ad1a7c99e4a665880f0 "https://github.com/krissnawat/airbnbclone-with-react-native/commit/b54a6e64bc8ce81981d24ad1a7c99e4a665880f0"). In the next chapter, we’re going to continue to implement our AirBnB clone app by adding animated checkmarks.

## credit

[Airbnb Clone using React Native Series by Cubui](https://www.youtube.com/watch?v=GF3WlD_p1lo "https://www.youtube.com/watch?v=GF3WlD\_p1lo")

