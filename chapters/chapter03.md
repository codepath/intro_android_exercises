---
layout: exercises
title: Chapter 3
---

## Chapter 3 - Views

### Exercise 1: Layout Gravity

**Goal**: Explore layout gravity.

**Description**:

In Chapter 2, we explored the gravity property. Layout gravity specifies the gravity of an element with respect to its parent. The easiest way to understand this is to try a few layout gravity options and see what happens.

**Directions**:

1. Open the layout XML.
2. Add at least three TextViews in a vertical LinearLayout.
3. For each TextView, add the android:padding property and set it to 30dp. This will create some space between the TextViews.
4. Set the android:layout_gravity property of the first TextView to "left".
5. Set the android:layout_gravity property of the second TextView to "center".
6. Set the android:layout_gravity property of the third TextView to "right".


#### Snippets

    // In activity, have three TextViews similar to below
    <TextView
        android:layout_gravity="center"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:padding="30dp"
        android:text="Gravity Center" />

### Exercise 2: Basic Views

**Goal**: Explore the basic views of an Android application.

**Description**:

While an Android application has many complex views, most complex views are comprised of the basic views, TextView, EditText, Button, ImageView, and ImageButton.

**Directions**:

1. Open the layout XML.
2. Ensure that the root layout is a vertical LinearLayout.
3. Add an EditText input field.
4. Add a Button.
5. Add an ImageView.
6. Add an ImageButton
7. Set the android:layout_margin property to 20dp to create some space between the elements.

#### Snippets

    // Hint: Switch to Graphical Layout and
    // drag the inputs from the left-hand palette

### Exercise 3: View Attributes

**Goal**: Explore view attributes and getting a handle to the view from Java.

**Description**:

Views have many different properties to configure their appearance and behavior. In this exercise, we will experiment will a few basic properties, such as setting the background color and playing with margin and padding.

XML is used to describe the static aspects of an Activity. However, we will often need to manipulate or access the views in Java as well. For example, if the user enters some input in an EditText view, we need to be able to access that EditText to find out what they entered.

For views that need to be accessed from Java, add a unique id label, using @+id/some_id. ONLY assign an id to views that need to be accessed from Java.

**Directions**:

1. Open the layout XML.
2. Set the properties of a TextView
   - android:background="#06327a"
   - android:textColor="#cbd9f0"
   - android:padding="15dp"
   - android:layout_margin="10dp"
   - android:layout_centerHorizontal="true"
   - android:layout_centerVertical="false"
3. Add a unique id to the TextView
   - `android:id = "@+id/main_text_view"`
   - Now you can reference the textview in Java with `findViewById(R.id.tvMain)`
4. In the activity's Java file
   - Get a handle to the TextView, as shown in the snippet below
   - Hover your mouse over TextView and Toast and click the option to automatically import packages.


#### Snippets

    // Java code in Activity
    protected void onCreate(Bundle savedInstanceState) {
      // ...
      TextView tvMain = (TextView) findViewById(R.id.tvMain);
      Toast.makeText(this, tvMain.getText().toString(), Toast.LENGTH_SHORT).show();
    }

### Exercise 4: Simple ListView

**Goal**: Explore a simple ListView.

**Description**:

Aside from the basic views, the ListView is the most common view when developing Android applications. If you think about the apps that you use, like Mail, Facebook, Twitter, Instagram, etc, so many views involve scrolling a list of custom views.

ListViews work in two parts: an adapter that provides access to an array of data, and a custom view template to style each individual item.

Android provides a simple default view template that is just a simple TextView, which is shown in the snippet below and referenced using R.layout.simple_list_view_item. This is fine for testing, but in the future we will use our own custom template.

**Directions**:

1. Create a new activity and set it to be the default launch activity.
2. In the layout XML
   - Add a ListView, setting the layout_width and layout_height to be `match_parent`.
   - `match_parent` means that the listview will be as tall and as wide as it's container.
3. In the activity's Java file, modify the `onCreate` method
   - Define an array of data
   - Create an adapter, specifiying the view template and the data array.
   - Attach the adapter to the ListView
4. Run the application

#### Snippets

    // res/layout/simple_list_view_item.xml
    <?xml version="1.0" encoding="utf-8"?>
    <TextView xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:padding="5dp"
        android:textSize="15sp"
        android:background="@drawable/simple_list_selector"
        android:layout_height="match_parent"
        android:textColor="#8ab1dd" >
    </TextView>

    // In Activity
    protected void onCreate(Bundle savedInstanceState) {
        // ...
        String[] myStringArray = { "Bruce", "Wayne", "Bill" };
        ArrayAdapter<String> adapter = new ArrayAdapter<String>(this,
          R.layout.simple_list_view_item, myStringArray);

        ListView listView = (ListView) findViewById(R.id.lvDemo);
        listView.setAdapter(adapter);
    }