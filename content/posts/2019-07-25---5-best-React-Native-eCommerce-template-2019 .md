---
title: Build a Medium-Style Clap Animation with React Native
published: true
tags: mobile-development,react-native,ui,heartbeat
canonical_url: https://heartbeat.fritz.ai/build-a-medium-style-clap-animation-with-react-native-c4f028e06495
cover_image: https://cdn-images-1.medium.com/max/1024/1*UTIvF72fNwgsdlY7XH_kiQ.jpeg
---

### Make a fully functional real estate app in minutes

Become the next Trulia, Zillow or Airbnb by releasing a real estate app for both iOS and Android in minutes. Download our functional [React Native Real Estate](https://www.instamobile.io/app-templates/real-estate-app-template-react-native/?ref=4094&campaign=dev.to) app template, integrated with Firebase Backend, to literally launch your own app today. Crafted with extreme attention to details, this beautiful app template written in React Native represents the best way to jumpstart the development of your new mobile app.

In this article, we’re going to learn how to build a Medium-style clap animation with React Native, including everything from initializing a React Native project to making the animation work properly.

This tutorial will cover every step in detail and include code snippets for each step. We’ll work through this tutorial by creating a new react-native project, downloading a clap image from Medium, and ending with the final animation that will include clapping, counting claps, hiding claps, etc.

Let’s get started.

### Bootstrap our app

First, we need to create a new React Native project. For that we’ll use the following command:

react-native init

Then, we need to grab the Medium clap image. You can download the image from the link provided in the image below:

![](https://cdn-images-1.medium.com/max/512/0*mDBWcpZf3sbfnE4J)<figcaption><a href="https://github.com/phuongtailtranminh/React-Native-Medium-Clap-Animation/blob/master/images/clap.png">source here</a></figcaption>

Next, we need to create a folder structure as shown in the screenshot below:

![](https://cdn-images-1.medium.com/max/251/1*lg0jcV_U08rxb8z8PV47CA.png)

As we see in the above image, the clap.png image file is in “img” directory, with the components directory containing the JS files.

We need to clear up the App.js file as shown below:

%[https://gist.github.com/krissnawat/943d12aaf6ded8eb9db0ebc066e1e93b]

Now we have a container for implementing a clap button and animation, as shown in the emulator screenshot below:

![](https://cdn-images-1.medium.com/max/432/1*woBX_D1dytXF0L5IM0eOSA.png)

### Prepare Clap Button

In this step, we need to open the clapbutton.js file in our IDE and then import the clap.png image file from the img directory of our project repository. Then we pull to the bottom of the view container. The components necessary for this are imported from the react-native package as shown in the snippet below:

%[https://gist.github.com/krissnawat/11dab2882ccdb3b6bd3434be42b2c8d4]

Here, we need to use a View component for the wrapper and TouchableOpacity to make an image that we imported seem like a button. Then, we need to add style to the image to it make look like the clap button from Medium. After this, we’ll get a clap button at the bottom-right corner of our emulator screen:

![](https://cdn-images-1.medium.com/max/432/1*zk8Bs_t46yKKNZcdIlyK-g.png)

> The next revolution in mobile development? Machine learning. Don’t miss out on the latest from this emerging intersection. [Sign up](https://www.fritz.ai/newsletter?utm_campaign=heartbeat-newsletter-fomo2&utm_source=heartbeat) for weekly updates from our crew of mobile devs and machine learners.

### Clap Bubble effect

Next, we need to add a bubble animation to the clap button with the Animated component. We import the Animated component from the react-native package and use it in the view:

%[https://gist.github.com/krissnawat/9f087fb47c0ce6bb23addd6764fbe684]

As a result, we’ll get the following animated object over the image in your emulator:

![](https://cdn-images-1.medium.com/max/476/1*ovUeexN3Vs2JEjXasxs_mg.png)

We can fix it by adjusting the CSS style and moving the Animated view component on top of the TouchableOpacity component:

%[https://gist.github.com/krissnawat/669aef52bc430b1b1de0e9f247d516af]

We can now see that the clap button overlaps the clap bubble:

![](https://cdn-images-1.medium.com/max/432/1*-waILWfZppVoCcDArz727A.png)

### Adding Animation

This step is probably a bit complex compared to the others. In this step, we’re going to add an animation to our clap button. First, we add an animation for clapbubble*.* By adding translateY, we move clapbubble over the clap button, and then we configure its opacity.

Here, we start by adding a bootstrap animation state value as shown in the code snippet below:

%[https://gist.github.com/krissnawat/b40ec81862eff3804630456472615129]

And then, we add it to the clapbubble Animated component:

%[https://gist.github.com/krissnawat/afe7b5e9410c98e044344732b83384f7]

Now, we need to add the time value for our animation. We can do this by adding an animation value with timing function :

%[https://gist.github.com/krissnawat/e639f2cfe1c8c2f788511c98cdf217ff]

Here, we’re using a parallel method to ensure the two animations work concurrently.

The result of the above code can be seen in the simulation of the emulator below:

![](https://cdn-images-1.medium.com/max/364/1*LKJ5GLHRfi0TOVYJlA15wA.gif)

### Adding Clap Count

In this step, we’re going to add clap count text to clapbubble that we implemented in the above steps. To do this, we’ll use the Text component from the react-native package. We’re binding the Text component with CSS style as well:

%[https://gist.github.com/krissnawat/afee6db4144ec12b03e7435da2a7b8f4]

Here, we hard code the count value before making a dynamic change to it. Again, we can check out the result in our emulator:

![](https://cdn-images-1.medium.com/max/476/1*zgckLmijIG6M5iWp_eKWTg.png)

Now, to make the count dynamic, we need to make our count value increase by a clap. To do this we need to create a new function to handle clap count.

First, add two new states to contain the count value, as shown in the code snippet below:

%[https://gist.github.com/krissnawat/f5a5f0250e8d86cf22300a93cea05937]

Then, we need to create a clap() function to handle the clap increment:

%[https://gist.github.com/krissnawat/d6f90692b06ec6e0aae2abeaddd13f61]

Now, we need to inject the clap() function into the clap button. We can do so by using the following code snippet:

%[https://gist.github.com/krissnawat/ee435691883fc06bf845575fa423d3e5]

Now, test if it works as shown in the web console and emulator simulation below:

![](https://cdn-images-1.medium.com/max/1024/1*DSVp3aKNNwgGm3fLW12U-Q.gif)

We use claps to contain the count to avoid multiple renders in the view by using the code snippet below:

%[https://gist.github.com/krissnawat/76ab509df735bfed990675fbf4d4d89e]

Now, we can see the result of the code in the emulator simulation below:

![](https://cdn-images-1.medium.com/max/1024/1*fry-EK8-iEEQwWVwCBNo5w.gif)

### Rendering Claps

In this step, we’ll make the clap re-render for animation purposes. The proper way to re-render a claps bubble is to make a new component for the clap bubble and then re-load the component multiple times when the clap is clicked. To do this, we need to create a component named ClapBubble and move all our clapbubble code to this component, as shown in the code snippet below:

%[https://gist.github.com/krissnawat/a574ce4fb1c45387d2580e5de87d40ec]

And then, we need to import everything to the ClapButton component:

%[https://gist.github.com/krissnawat/5094ec4246b3e492807ab0ea1b067e6f]

In order to re-render claps, first, when we hit the clap button, the clap value updates in the clap() function. Then, the updated state chains to the renderClaps() method, making the ClapBubble component reload with maps. Lastly, we call the renderClaps() function in the wrapper to make them re-render every time when we hit clap.

The result can be seen in the emulator simulation below:

![](https://cdn-images-1.medium.com/max/364/1*V97G7jactwlCPODKAxmgkA.gif)

Next, we update the clap value by passing count value to the ClapBubble component. We can do this by using the code snippet below:

%[https://gist.github.com/krissnawat/bdaf56709ef7129503a71e2083b352f5]

And then we need to update the ClapBubble component as shown in the snippet below:

%[https://gist.github.com/krissnawat/51c8652c2697df05073540d3c721b90a]

We can see below that the count value increases every time we click the clap button with an animation:

![](https://cdn-images-1.medium.com/max/364/1*8M_8okGdE40QDxFi-Dmrow.gif)

### Hiding the ClapBubble after clapped

After we click on the clap button, we can see that the clapbubble with the animation doesn’t hide and instead keeps showing itself in the view. In this step, we write some code to hide this clapbubble with a clap operation that’s completed by the user.

First, we need to open the ClapButton.js file and then add the function given in code snippet below:

%[https://gist.github.com/krissnawat/9178be895a389070b59fd07db771858d]

Here, we remove the count clapbubble when the animation has successfully rendered. Next, we pass it to the ClapBubble component:

%[https://gist.github.com/krissnawat/b180d325a72b7a216494e58b83636eaf]

Now we need to open the ClapBubble component and paste the code below:

%[https://gist.github.com/krissnawat/802bc3b380e2e5cd35c5d1b37b1faea5]

Next, we delay the removal of the clapped bubble by 500 ms, which will make the animation look nice and smooth. We can see the result in the emulator simulation below:

![](https://cdn-images-1.medium.com/max/364/1*bIBIw4HAoU1bUJgPcCCxwQ.gif)

### Keep Clapping

Here, we add our last feature to allow users to keep clapping when they hold the clap button. The clap bubble should render multiple times until we release the mouse.

#### Initiate keep clapping

First, to keep clapping, we need to repeatedly call the clap() function with setInterval as shown in the code snippet below:

%[https://gist.github.com/krissnawat/8bff056c824d9a73f845f1104c1b3947]

Then we add the keepClapping() function to ClapButton with and OnPressIn event as shown in the code snippet below:

%[https://gist.github.com/krissnawat/0d6a7020a1205563f7d215c9571c84c8]

Let’s keep clapping to see the result:

![](https://cdn-images-1.medium.com/max/364/1*ohB6I5UnBJUsKapHUYfzIQ.gif)

But as we can see, now we can’t stop the clapping! So we need to add a stopClapping() function.

#### Stop keep clapping

We need to add one more function named stopClapping(), which will have a clearInterval() function to remove the interval object:

%[https://gist.github.com/krissnawat/30e5b9eb1bea54996856133d328acd3a]

Finally, we activate with an onPressOut event to trigger the stopClapping() function:

%[https://gist.github.com/krissnawat/8c728a2c0cd03b875218d684daacbb79]

And there it is! We have our final result, which you can observe in the simulation below:

![](https://cdn-images-1.medium.com/max/364/1*Si-wzYCechMZJgqaZooWpg.gif)

### Recap

In this post, we learned how to use many React Native Animated components and functions like timing, start, translate, opacity, etc. By using these components and functions, we learned how to implement a real-world example of the clap button that’s similar to Medium’s “Clap” feature. You can find all the code on GitHub:

[krissnawat/react-native-medium-clap-clone](https://github.com/krissnawat/react-native-medium-clap-clone)

#### Resources

- [React Native Animations Tutorial — Learn by building Medium’s claps animation](https://www.youtube.com/watch?v=Xe7F6Hdss9k&t=590s)
- [React-Native-Medium-Clap-Animation](https://github.com/phuongtailtranminh/React-Native-Medium-Clap-Animation)
