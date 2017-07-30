## Using views from Activities
Now that you know how to build an activity and a layout file, it's time to put everything together. In this tutorial we'll go over how to reference and work with views inside an activity.  

### Referencing Views
Android activities have a handy method called `findViewById()` which returns a view given it's id. It returns a generic view object, but you can cast it to the correct subclass.

Here's an example. Let's say you have a textView defined like this:

```xml
 <TextView
	android:id="@+id/my_textview"
    android:layout_width="200dp"
    android:layout_height="75dp"/>
```

You could get a reference to that TextView from inside the `onCreate()` method of your activity. Here's how:

```java
@Override
public void onCreate(Bundle savedInstanceState) {
  super.onCreate(savedInstanceState);
  setContentView(R.layout.activity_main);
  TextView myTextView = (TextView)
  findViewById(R.id.my_textview);
  
  //Now we can work with myTextView
  myTextView.setText("Hello World!");

}
```

As you can see, the `findViewById()` method returns a reference to the view who's id we passed in. Although the return type of the method is a `View`, we can safely cast it to a `TextView` because we know the type already. From there, we can call all sorts of different methods to interact with our TextView. In this case, we use `setText()` to set the text content of the view.

### Registering Callbacks

Callbacks are an important part of working with many types of views. A lot of times we want to be able to say "please run this code when the user does x, but don't run it right now". That's exactly what callbacks allow us to do.

Let's set up another example. First, you can grab a reference to a button just like before. Next, you can use the `setOnClickListener()` to register a callback. When the button is clicked, whatever code you pass in to this method will be run. In this example, we update the button's text once it's been pressed:

```java
Button myButton =(Button) findViewById(R.id.my_button);
myButton.setOnClickListener(new View.OnClickListener() {
	@Override
	public void onClick(View v) {
		//This will be run when the user clicks a button
		myButton.setText("You clicked me!");
	}
});
```

Buttons are the most obvious time when you would want to register a callback, but most views have a few different callbacks to can register if needed. In most cases these are just optional, though.


### Organizing your activity

The standard way to organize your activity is to create a class-level field for each view you intend to work with, and then set those variables in `onCreate()`. This allows us to call `findViewById()` just once per view element, and then re-use those variables later in other methods for our activity. Although you don't initialize the values in a constructor, `onCreate()` always runs first, so you can safely reference the variables without worrying if they're null.



```java
public class MainActivity extends Activity {
//We define our views as class fields
Button myButton;
TextView myTextView;

@Override
protected void onCreate(Bundle savedInstanceState) {
	//Run the normal onCreate() method first
	super.onCreate(savedInstanceState);

	//Load an interface for the activity
	setContentView(R.layout.activity_main);
	//Assign our vars
	myButton = (Button) findViewById(R.id.my_button);
	myTextview = (TextView) findViewById(R.id.my_textview);
	}

	@Override
	protected void onResume() {
		//Now we can re-use these vars if needed
		myTextview.setText("Bye");
	}
}

```
