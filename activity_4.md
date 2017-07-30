## Common Android Views
There's many different types of views, but a few are used a lot more than others. Understanding those basic views is a pretty important step in learning Android. We'll go over those quickly in this lesson.

### TextViews
`TextViews` are one of the most simple views-- All they do is render some text on the screen. You can use the `setText()` method if you want to set the text inside your activity. This is great for situations where you need to update the label based on something the user has done.

Here's some of the more common attributes:

| Attribute     | Effect                                   |      |
| ------------- | ---------------------------------------- | ---- |
| text          | The text value to show in the TextView   |      |
| textStyle     | The style of front to use (e.g. bold/italic) |      |
| fontFamily    | The font to use for the text             |      |
| textAlignment | How to align the text within the view (center, left, top, etc...) |      |

### Buttons
`Buttons` are a pretty common part of any android app. Just like a textView, they have a text value which is displayed over the button. Clicking a button will do nothing by default, but you can register a callback using `setOnClickListener()`.


```java
myButton.setOnClickListener(new View.OnClickListener() {
	@Override
	public void onClick(View v) {
		//This will be run when the user clicks a button
		myButton.setText("You clicked me!");
	}
});
```
Another common method is `setEnabled()` , which allows you to mark the button as either enabled or disabled. This is great for times when you want to disable a button until something else happens. For example, you might want to disable a login button until after a user has entered their password in another field.

It's actually possible to define a callback using the `onClick` property in the button's layout file. However, it's generally preferred to use  `setOnClickListener()` since it works with older devices and keeps all your business logic on one place.

### EditTexts
`EditTexts` are editable text boxes that the user can type in. These are great for accepting any type of text-based user input like emails or passwords.

Typically EditTexts don't have much behavior on their own. Instead, you usually just read their values from some other callback with `getText()`. One quirk of EditTexts is that the `getText()` method actually returns an `Editable` object instead of a string, but you can use `toString()` to easily convert it. Like a button, you can use `setEnabled()` to lock or unlock the textview for editing.

```java
String myText = myEditText.getText().toString();
myTextView.setText("The user entered" + myText);
```
Here's some of the more common attributes:

| Attribute | Effect                                   |      |
| --------- | ---------------------------------------- | ---- |
| hint      | The "hint" text to show before the user starts typing |      |
| inputType | The type of input (e.g. number, text, password,email). Android will show the appropriate keyboard type. |      |
| maxLines  | The number of lines in the input box (defaults to 1) |      |
