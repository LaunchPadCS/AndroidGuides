## Android Development Overview
Mobile apps are more popular than ever, which makes knowing how to build Android apps a great skill to have. Building a mobile app can require a pretty different skill set than building a web application, but once you get the basics down the rest is relatively easy to pick up.

There's a lot of different parts that go into making an Android app. In this series of lessons, we're just going to go over the basic structure of an app as well as go through a few examples.

### Android Development Requirements

Before hopping into Android development, it's important to make sure you've got what you need to be successful with it.

First, building an Android application requires at least a basic understanding of `Java`. If you are completely new to Java, you should learn the fundamentals before jumping into Android.

Second, it really helps if you own an Android phone. It's not technically required because you can set up an emulator on your laptop, but it's much more difficult than just using a real phone.

You can build Android apps on any type of laptop. The tools you'll need are all available on PC, mac, and Linux.


### Android Architecture
Building a program that can interact with hardware on a device can be very complicated, especially since every Android phone can have different parts. To solve this problem, Google has created the `Android API Framework` which is included as part of every android phone. Developers call methods defined in this framework, and then Android handles the rest.

In other words, the key to learning how to develop for Android is just learning all the different features of the Android API Framework. It's a massive system, but luckily you only need to understand a few key parts to make a simple app.

This handy diagram from Google shows how the whole system works together. It's pretty complicated, but the good news is that you only need to worry about the very first two layers.

![Android Stack](https://google-developer-training.gitbooks.io/android-developer-fundamentals-course-concepts/content/en/images/1_0_C_images/dg_android_stack.png)

### Versions of Android
One of the not-so-fun parts of mobile development is dealing with devices all running different operating systems. If you use an iOS device, you might assume that most people just run the latest operating system. Unfortunately, that's not the case with Android. At the time of writing, only 4.9% of Android users are using the latest operating system (Nougat).

So, how do you deal with trying to make an app that will work on 10 different operating systems? Luckily, each new version of Android provides compatibility tools so that older phones can still use those features. When you start building an app, you pick the version of Android you want to base it on. The newer the version you pick, the more  features you get, but the harder it is to make sure it works on older devices. Fun stuff!
