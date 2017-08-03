## Android Layout Files
A pretty important part of any Android app is the interface that the user will see. In this lesson we'll briefly go over how to create a simple interface.

### What is a Layout File?
When an activity is launched, you call `setContentView()` to tell Android to load up a layout file for your activity. Whatever interface is specified in that file will automatically be built and displayed to the user. Layout files are written in `xml`. As the name implies, they *only* specify a layout. A layout file does not contain any of the main logic for your app.

A layout file is created from `Views`. A view is just a type of object that you can render onto the screen. Views are things like buttons, text boxes, lists, or checkboxes. There's also  `View Groups` (also called `Layouts`), which aren't visible to the user, but instead contain other views.  Every Layout file will use one View Group as it's root, but it could contain many.

Here's a list of the common Layouts:
* A `LinearLayout` is a group of views lined up one after another, either horizontally or vertically
*  A `RelativeLayout` is a group of views where each view is positioned relatively to other views. You can say things like "this button is 10px below that other button".
* A `GridLayout` places it's views in a rectangular grid which can be scrolled through. This is great for things like lists.

This diagram shows how a LinearLayout containing 3 views might be rendered onto a device:

![Layout example](https://google-developer-training.gitbooks.io/android-developer-fundamentals-course-concepts/content/en/images/1_2_C_images/dg_layout_diagram_and_hierarchy.png)



### The Layout Editor

When you open a layout file inside Android Studio, you'll see a rendering of the view on your screen.

![Layout Editor](https://google-developer-training.gitbooks.io/android-developer-fundamentals-course-concepts/content/en/images/1_2_C_images/as_exploreeditor.png)

The editor might look a little different on your computer, but the windows you see should be the same. The parts of the editor are as follows:

1. The selected layout file
2. A list of views which can be used in this layout
3. An options toolbar to configure a few different settings
4. The properties pane, which shows the different properties for each view
5. The individual property you want to edit
6. A rendering of what the actual view will look like
7. A tree that lists all the different views in the layout
8. The design toggle. You can switch this off to edit the raw xml.

Most of the time, it's easier to switch the design toggle off and directly edit the xml files. Then, you can switch back to design mode to check what your view looks like.

### An Example
The layout file itself is made from several different xml tags. In order to nest views inside another view, you just place the child tag inside the parent.

Here's an example of a LinearLayout with a button and textView inside it:

```xml
<LinearLayout
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <Button
        android:id="@+id/button_toast"
        android:layout_width="@dimen/my_view_width"
        android:layout_height="wrap_content"/>

    <TextView
        android:id="@+id/show_count"
        android:layout_width="@dimen/my_view_width"
        android:layout_height="@dimen/counter_height"/>
</LinearLayout>
```
Note that each tag can have attributes defined on it. In this case, `android:layout_width` and `android:layout_height` are used to define the width and height of each view.

One important attribute is the `id`. You can use the syntax  `@+id/my_id_here` to define an id on a view. This allows you to reference this view from inside your activity.
