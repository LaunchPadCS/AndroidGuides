## Network Requests in Android
Communicating with the internet is a pretty important of many Android apps. In this lesson we'll go over the basic principals of android networking and go through some simple examples.

### Networking and Threading in Android
Before diving into networking, it's important to understand how Android apps handle `Threads`. If you haven't worked with threads in other languages before, you may want to skim through [this](https://howtoprogramwithjava.com/java-multithreading/) article on Java threads. Either way, the basic idea of threads is that a device with a multi-core processor can run multiple lines of code at the same time. Portions of code that run on different threads at the same time are called `Asynchronous`.

In Android, all your code runs on the `Main Thread` (also known as the `UI Thread`) by default. This means that if you make a function that takes 5 seconds to finish, your app will appear frozen for that entire time. This is called blocking the main thread, and it's generally something you want to avoid.

So how does that apply to networking requests in Android? Requests to servers on the internet can often take several seconds to complete, and we don't want the app to be frozen while we wait. That means that whenever you make a network request, it must not run on the main thread. The Android runtime actually enforces this as a rule-- if you try to make a networking request on the main thread, an exception will be thrown and your request will fail.

One other rule android enforces is the networking permission check. When users install your app, they need to agree to grant whatever permissions you ask for. To request a permission, you need to list it in the `app/src/main/AndroidManifest.xml` file.

For internet access, you can just add this line at the top of the file, right under the manifest tag:
```xml
<uses-permission android:name="android.permission.INTERNET"/>
```

### OkHttp Basics
Handling all of that network logic yourself can get a little crazy, so many Android developers will use a helper library to make things easier. We recommend [OkHttp](https://github.com/square/okhttp), since it's pretty powerful but also easy to set up.

Adding external libraries to android is super easy! All you usually need to do is add a single line to your  `app/build.gradle` file (NOT the `build.gradle` file in the root directly of your project).

For OkHttp, you just add this line under the "dependencies" section:

```
compile 'com.squareup.okhttp3:okhttp:3.8.1'
```

After editing the file, Android Studio will ask you to sync. Just say yes and OkHttp will be automatically downloaded and added to the project.


### An Example
We'll set up our app to check in with the [YesNo](https://yesno.wtf) api. If you visit their [api page](https://yesno.wtf/api), you'll see a yes or no answer along with a link to a funny gif message. We'll set up our app to visit this page and print our the response.

OkHttp accepts a `callback` from us, just like the callbacks we used earlier for clicking buttons. By setting this callback, OkHttp is promising to run our function once the network request finishes. Unlike the button click callback, network requests can fail. To deal with this, the callback has an `onFailure()` and `onSuccess()` method, and OkHttp will call whichever one is appropriate.

This code would just receive the response and print it to Android Studio's logcat console:
```java
//Build an OkHttpClient
OkHttpClient client = new OkHttpClient.Builder().build();

//Build our request and set the URL
Request request = new Request.Builder()
        .url("https://yesno.wtf/api")
        .build();

//Execute the request and pass our callback
client.newCall(request).enqueue(new Callback() {
    @Override
    public void onFailure(Call call, IOException e) {
	    //If this runs, something went wrong
        Log.e("MyApp","Oh no! Something went wrong!" + e.getMessage());
    }

    @Override
    public void onResponse(Call call, Response response) throws IOException {
	    //If this happens, we heard back from the server!
        Log.d("MyApp","We got an answer back: " + response.body().string());
    }
```

If you wanted to, you could take some other actions based on the result. For example, you could break down the response and then display the result in a popup to the user. However, one important thing to keep in mind is that your callbacks are not running on the main thread. Since only code running on the main thread is allowed to update the UI, you would not be able to directly call `setText()` here. Instead, you would need to use the `runOnUiThread()` method described [here](https://developer.android.com/reference/android/app/Activity.html#runOnUiThread%28java.lang.Runnable%29) ([example](https://stackoverflow.com/a/27992603/4171588)). 
