## Android Activities
It's time to hop into some actual programming now! The first concept you'll want to become familiar with is Activities. We'll briefly cover the basics in this lesson.

### What is an Activity?
An activity represents a single "screen" in your app as well as an interface the user can interact with. For example, a phone app might have one activity for the number dialing screen, and then another for the contacts list screen. One important concept to understand is that even though an app is made up from many Activities, those activities operate independently of each other, and only one can be active at once.

Unlike a standard Java program, you do not specify a `main()` method for the program to start. Instead, you specify a `Main Activity` to be launched automatically when the user runs the app. That activity can then launch other activities if needed.  When the user presses the back button, the current activity will be closed and the previous one will be resumed.


### The Activity Lifecycle

Your app is just one of many on the user's phone. At any time, they could minimize your app, receive a phone call, or lock the phone. It's even possible for Android to shut down your app unexpectedly if the phone starts to get too overworked. To help deal with these situations, it's important to understand the `Activity Lifecycle`. The lifecycle is a flow chart of all the different states your activity could be in, all the way from starting up to when it's finally closed.

Take a look at the [official diagram](https://developer.android.com/guide/components/activities/activity-lifecycle.html) below to get an idea of how this process works:

![Android Activity Lifecycle](https://developer.android.com/guide/components/images/activity_lifecycle.png)

At each stage of the lifecycle, the Android runtime will automatically trigger the methods shown in that diagram. For example, when an Activity starts up for the first time the `onCreate()` method will *always* be called, followed by calls to `onStart()` and `onResume()`. On the other hand, you are guaranteed that `onPause()` will always be called if the app is being moved out of the foreground for any reason.


### An Example Activity

Every activity is a single class which extends the base Android Activity class. You may override any of the lifecycle methods, but it's not required. If you don't specify any behavior for a lifecycle method, Android will just handle it automatically.

A very simple activity might look something like this:


```java
public class MainActivity extends Activity {
   @Override
   protected void onCreate(Bundle savedInstanceState) {
	   //Run the normal onCreate() method first
       super.onCreate(savedInstanceState);

       //Load an interface for the activity
       setContentView(R.layout.activity_main);
   }
}

```

That's all you need to create a simple activity! Note that the `setContentView()` method lets Android know which interface we want to use for this activity. We'll get to that more in the next lesson.

One small detail that we glossed over earlier is the `Android Manifest` . The manifest is an xml file in your app which lists all the activities you have set up. This is also where you tell Android which activity you want to start first. Android Studio actually handles this automatically, but if you're curious, here's what the file would need to look like if you were writing it yourself:

```
<activity android:name=".MyMainActivity" >
   <!--Tell Android we want this start automatically-->
   <intent-filter>
      <action android:name="android.intent.action.MAIN" />
      <category android:name="android.intent.category.LAUNCHER" />
   </intent-filter>
</activity>
```
