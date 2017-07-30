## Passing data with Fragments
Now that you know the basics of how to create a fragment, we can work through some examples of actually doing things with fragments. A lot of this is similar to working with activities, but things can be slightly different.

### Inflating views
You build your fragment's views in the `onCreateView()` method like we discussed earlier. However, you may have noticed that there is no `findViewById()` method in the fragment class. This makes it a little harder than normal to get a reference to a view (like a text box) that we may want to change. The trick is to use the inflated view object to get the references you need.

Here's an example:


```java
public class MyFragment extends Fragment {
	EditText myEditText;
	@Override
	public View onCreateView(LayoutInflater inflater,
		ViewGroup container,Bundle savedInstanceState) {
		//Store the view instead of returning
		View myView = inflater.inflate(R.layout.my_fragment_layout, container, false);
		//Use the view object to find our edit text
		myEditText = view.findViewById(R.id.my_edit_text);

		//Now we can return the view to be rendered
		return myView;
	    }
}
```

### Factory method arguments
In the last section we briefly touched on using `Factory Methods` instead of normal constructors for fragments. These are very helpful for situations when we want to pass in some arguments to a fragment. Let's say we wanted to make a fragment that shows a welcome message to the user, and we want that welcome message to be passed in by the activity.

First, we would accept that message as an argument in our static factory method. In the factory method, we can store that message for later using the `args.putString()` method. You need to add a name for the argument so it can be identified later, so we'll use "message_arg" as the name.

Second, we use the `getString()` method inside our fragment's `onCreate()` method. When calling `getString()` we just need to pass in the same tag we used earlier ("message_arg") to load the data. From this point we could now use this string in our fragment for whatever we wanted.

```java
public class MyFragment extends Fragment {
	String myMessage;

	//Our factory method
    public static MyFragment newInstance(String myMessage) {
        MyFragment fragment = new MyFragment();
        Bundle args = new Bundle();
        args.putString("message_arg", myMessage);
        fragment.setArguments(args);
        return fragment;
    }

	@Override
	public void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		if (getArguments() != null) {
			myMessage = getArguments().getString("message_arg");
			//Now we can do whatever we want with myMessage in this fragment
		}
	}
}
```

This works with all sorts of arguments, not just Strings. You can also add multiple parameters instead of just one, as long as you make sure to keep the tags you use unique.

### Talking to activities from fragments
Fragments make it easy to pass data around. Sometimes you'll want to have one "parent activity" that switches between multiple fragments as the user moves around the app. Let's say that you have one fragment where the user will select some options and then press a button. When the button gets pressed, you'll save their choices in the activity and then switch to the next fragment.

The `getActivity()` method will return the activity that this fragment is attached to. This is great for times when we want to talk to the parent activity from the fragment. Always remember that this method can return null, since it's possible the fragment is not attached to an activity.


```java
public void storeData() {
	Activity parentActivity = getActivity();
	//Make sure this is set
	if(parentActivity == null) {
		return; //Oh no, we're not attached!
	}
	//Make sure we're attached to the activity we expect
	if(parentActivity instanceof MyMainActivity) {
		//It's safe to cast
		MyMainActivity activity = (MyMainActivity)parentActivity;

		//Now we can directly call methods on the parent
		activity.storeMyData("Some Data");
		activity.doSomeThings();
	} else {
		//Uh oh, somehow we got attached to the wrong thing!
	}
}
```

We  can also use a similar system to swap between fragments. One fragment can call a method in the parent activity that will trigger a fragment swap. The main difference between swapping fragments and creating the first one is that we use the `replace` method instead of the `add` method.

Here's an example:

```java
public void openDifferentFragment() {
FragmentManager fragmentManager = getFragmentManager();
        fragmentManager.beginTransaction()
                .replace(R.id.container, SomeNewFragment.newInstance())
                .commit();
}
```

Hopefully after reading through this section, you have a better idea of how you can actually work with fragments. If you still want to get a better idea of how fragments work, you may want to take a look at the [Official Guide](https://developer.android.com/guide/components/fragments.html). 
