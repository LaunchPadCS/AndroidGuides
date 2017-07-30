## Fragments
Although Activities are the basic building blocks of Android, Fragments are another powerful tool that you can use to structure your app. We'll go over the basics of fragments and why you might want to use them in this lesson.

### What is a fragment?
`Fragments` are classes that represent a chunk of the UI (and it's associated behavior) inside an Activity. Up until now we've always talked about activities with only one main function, but that's not always going to be the case. A good way to picture fragments is to think of them as mini-activities that live inside an actual `Activity`.

You might be wondering why we would want to use a fragment inside an activity when we could just use an activity. Here's a few of the main reasons:

1. Fragments make it easy to re-use layouts and functionality on devices of different screen sizes (e.g. tablets)
2.  Fragments make passing data between your views much easier
3. Fragments make building a UI much easier (e.g. tabbed views)

For example, on a mobile app you might have a list of settings. When the user clicks on a setting, the app opens up a second screen with details for that setting. On a tablet, there's plenty of room to show both screens at the same time. If you make each of those screens a fragment, then this change is easy to set up.

![Tablet Fragment Diagram](https://developer.android.com/images/fundamentals/fragments.png)

Because you can have multiple fragments inside the same activity, passing data between them becomes much easier. Any information that the fragments need to share can just be stored inside the parent activity.

### Fragment Lifecycle

Like activities, fragments have a lifecycle with different lifecycle methods that you can override. To start with, fragments have most of the same methods contained on Activities, like `onCreate()`, `onStart()`, and `onStop()`. When those methods are called in the parent activity, they will also be called in the fragment. This makes sense, because if the user closes an activity then the fragments it contains would also be closed.

However, fragments also have a few additional lifecycle methods, which are:

* `onAttach()` , which  is called when the fragment is linked with an Activity
* `onCreateView()` is called when Android wants to render the fragment's layout file
* `onActivityCreated()` is called once the parent activity is finished running `onCreate()`. This is useful for if you need to wait for the parent to get set up first.
* `onDestroyView()`, which is called when Android wants to destroy the fragment's view
* `onDetach()` is called when the fragment is being un-linked from an Activity.

As the activity changes state, all of it's fragments will be forced to change state as well. You can see this in the flow chart below:

![Fragment Lifecycle](https://developer.android.com/images/activity_fragment_lifecycle.png)

### An Example
All of that discussion might be a little hard to put together without an example, so we'll quickly put together a simple activity with a fragment.

First, you would have to build the fragment. You create a layout file for it just like you would for an activity. Next, you override the basic `onCreateView()` method to build the view.

 Fragments cannot just call `setContentView()`. Instead, Android will pass in a `LayoutInflater` parameter which you can use to build the view.

```java
public class MyFragment extends Fragment {

	@Override
	public View onCreateView(LayoutInflater inflater,
		ViewGroup container,Bundle savedInstanceState) {
		// Inflate the layout for this fragment using the super
		return inflater.inflate(R.layout.my_fragment_layout, container, false);
	    }
}
```

The standard convention in Android is to use a `Factory Method` to create your fragments. It's not required, but it helps keep things organized when your fragment needs to accept some input. A factory method is a just a static method inside a class that builds an instance of that class. In our case the fragment won't accept any parameters, but we'll use one anyways:

```java
public class MyFragment extends Fragment {
    public static MyFragment newInstance() {
        MyFragment fragment = new MyFragment();
        Bundle args = new Bundle();
        //Here we would set the args if we had any
        fragment.setArguments(args);
        return fragment;
    }
}
```
That's all we need to worry about in the fragment for now.  Next, you need to define a view inside your activity which will be a placeholder for the fragment. A `FrameLayout` is usually used for this:

```xml
<!-- The layout file for the activity -->
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="horizontal"
    android:layout_width="match_parent" android:layout_height="match_parent">

    <!-- The view where the fragment will be placed-->
    <FrameLayout android:id="@+id/myFragmentView"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>
</LinearLayout>
```

Finally, just override the `onCreate()` method inside the activity. Here, you build the fragment and then add it to the view. Don't worry about the specifics of how this works for now, as we'll go into more detail later. The important thing to understand is that a fragment is created with with the `newInstance()` call, and then that fragment is attached to the activity on the view you specify.

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);

	//First, create a new instance of the fragment
	MyFragment myFragment = MyFragment.newInstance();

	//Place the new fragment in the myFragmentView
	getFragmentManager().
		.beginTransaction()
		.add(android.R.id.myFragmentView, myFragment)
		.commit();
}
```

And that's it! Whatever view you built inside your fragment's `onCreateView()` method is what you'll see when you load up the activity. This was a simple example, but we'll go over making fragments actually function in a later section. 
