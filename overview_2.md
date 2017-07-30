## Android Development Tools
Before moving forward with Android development, it's a good idea to quickly go over some of the different tools you'll be using. This lesson just goes over the basics, and it's not super important that you understand all the details for all these tools.

### Android Studio
First things first is `Android Studio`. Until a few years ago, there was actually no official IDE for Android. Luckily for you, Google finally released [Android Studio](https://developer.android.com/studio/index.html) and it makes life much easier.

If you've used IntelliJ (or any other IDE) before, this is exactly the same idea. If not, just know that an IDE is like a sort of super text editor. It lets you edit and save files, but it also does lots of fancy things like autocompletion. In the case of Android Studio, it lets you easily send your app from your laptop onto your phone with a single button.

### ADB

`ADB` stands for the [Android Debugging Bridge](https://developer.android.com/studio/command-line/adb.html). It's a command line tool that has a lot of handy functions for working with real android devices. You probably won't need to mess with ADB too much for now (especially since Android Studio does a lot of this work automatically now), but it does have a few helpful tools. For example, you can use ADB to copy files between the phone and your computer. You can also do lots of fancy stuff with networking and debugging, but again, you don't need to worry about that too much for now.

### Emulators and AVDs
Testing your app on a real Android phone is always preferred to testing on an emulator. It's a lot faster and also a much more accurate way of testing. However, it's important to test your app on lots of different types of phones. Since buying every Android device in the world is too expensive, you can use an `emulator` to run a simulation of an Android phone on your laptop. If you have an Android phone, you won't need to worry about emulators until it's time to start testing your app for release.

Most people will just use the word `emulator` here, but technically these programs are called `Android Virtual Devices`, which is abbreviated `avd`. If you see somebody talk about setting up an `avd`, they just mean an Android emulator.

### LogCat
`LogCat` is the tool Android uses to collect system debug and error messages. You can access it through adb in the command line, but that can be a little bit of a pain. Luckily, Android Studio handles this automatically as well.


![Logcat](https://google-developer-training.gitbooks.io/android-developer-fundamentals-course-concepts/content/en/images/1_1_C_images/as_android_monitor_annotated.png)

1. You can use the `Log` class in your code to create a log message
2. The message will then appear in logcat

Logcat has several levels of debug messages, which you can use to represent messages of different severity. You can use the filter in the Logcat window to hide low-priority messages to help keep things organized.

Here's a list of the severity levels in increasingly severe order:

| Level   | Method    | Description                              |
| ------- | --------- | ---------------------------------------- |
| Verbose | Log.v()   | The lowest-priority message type. Should never be left in a published app. |
| Debug   | Log.d()   | A low-priority debug message. Generally should not be included in a published app. |
| Info    | Log.i()   | An information message to represent some important behavior. |
| Warning | Log.w()   | A message warning of an unusual (but not necessarily bad) event. |
| Error   | Log.e()   | Used when an error or undesired behavior has happened. The highest level of logging you should normally use. |
| Assert  | Log.wtf() | Used only when a situation occurs that should never happen under any circumstances. Calling this method will dump the logs and then kill the app. You probably shouldn't ever use this. |

The Log functions actually take two parameters-- a tag and the message. The tag is just a string to represent the "section" of your program printing the message. It's useful so that you can filter messages if needed. Most programmers just define a static `TAG` variable in each class and then use that in their log messages. 
