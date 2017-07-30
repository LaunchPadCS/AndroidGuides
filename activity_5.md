## Android ListViews
The `ListView` is a really common part of many Android applications, but it's a little trickier than other views to set up. In this lesson we'll go over the steps that go into creating a simple Android ListView.

### ListView Basics
`ListViews` are one of the important types of views in a mobile app. A ListView is a scrollable list of items, where each item can be clicked individually. You might have a list of emails where you can click on a specific item and see some details. A ListView is a sub-class of the more generic `AdapterView`.

Every type of AdapterView (including the ListView) requires some kind of  `Adapter` in order to function correctly. An Adapter is a class that takes a data source and is able to create views for each item in the source. For example, your data source might be a list of movies showing at your local theater. Your adapter would take that list and then create an individual view for each movie in the list. Finally, the `ListView` would actually display all those views in a nice scrollable list.

Here's a breakdown of all the different parts:

![Adapter Diagram](http://i.imgur.com/ecBxqTP.png)
1. A data source. Normally an ArrayList.
2. An Adapter which converts the data into small individual views
3. Individual views which are created by the adapter
4. The ListView, which contains all the individual views

### An example ArrayAdapter

Let's say we wanted to make a ListView that displays a list of movies from some data source. The most important method is  `getView()`. As the user scrolls through your list, the ListView will automatically call this method with the correct position number passed in. So if the ListView decides it needs to render item #5, then it will call `getView` with the position set to 5.

The one confusing part about the `getView()` method is the `convertView` parameter. Building views is relatively slow, so if the user scrolls quickly through a list it can cause the phone to lock up while building 50 different views. To deal with this problem, Android actually recycles old views by shuffling the order around internally. If the `convertView` parameter is not null, it's like Android is saying *"please use this view instead of inflating a new one, I'm way too busy right now"*.

Here's a basic example. We're assuming we have a Movie class with information about movie names and prices.

```java
public class MovieAdapter extends ArrayAdapter<Movie> {
    //A constructor which just calls the super to store our list
    public MovieAdapter (Context context, ArrayList<Movie> users) {
       super(context, 0, users);
    }

    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
       //Load the data item that's being asked for
       Movie movie = getItem(position);
       // Does android want us to recycle an old view?
       if (convertView == null) {
          //No, we need to make a view from scratch
          //We'll inflate the itemview_movie layout
          convertView = LayoutInflater.from(getContext()).inflate(R.layout.itemview_movie, parent, false);
       } else {
          //Android has given us a view to recycle, we don't need to make one ourselves
       }
       // Grab references to our view
       TextView movieTextView = (TextView) convertView.findViewById(R.id.movieTextView);
        TextView priceTextView = (TextView) convertView.findViewById(R.id.priceTextView);
       // Update the data in the view to match the data object
       movieTextView .setText(movie.name);
       priceTextView.setText(movie.price);
       // Return the completed view to render on screen
       return convertView;
   }
}
```

### Hooking things up

An adapter doesn't do anything until it's connected to a data source and a listView. Luckily, it's easy to do this:

```java
// Construct the data source
ArrayList<Movie> myMovieArray = new ArrayList<Movie>();

//In a real app we would update myMovieArray with movie info from the internet here

// Create the adapter and connect it to our data source
MovieAdapter myAdapter = new MovieAdapter (this, myMovieArray);

// Connect the adapter with the ListView
myListView.setAdapter(myAdapter);
```

And that's all you need to get a basic list view up and running. One final thing to keep in mind is that the adapter doesn't magically know if you add or remove items from the movie list. There's two options for dealing with this:

1. Whenever you modify the underlying array, you must call the `notifyDataSetChanged()` method on the adapter to let it know that it should refresh itself.
2. Instead of modifying the underlying array, you call the `add()` and `remove()` items directly on the adapter. This will insert the new item into your view and automatically refresh.

Although the example we went over here used a ListView and an ArrayAdapter, there's many different types of AdapterViews and Adapters. Luckily, the basic idea is exactly the same for all of those different types.

### Recommended Reading

[Using an ArrayAdapter with a ListView](https://github.com/codepath/android_guides/wiki/Using-an-ArrayAdapter-with-ListView)
