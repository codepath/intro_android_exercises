---
layout: exercises
title: Chapter 2
---

## Chapter 2 - User Interface

### Exercise 1: Launcher

**Goal**: Create a new activity and set it to be the default activity.

**Description**:

Every activity in the project must be listed in AndroidManifest.xml, in the application node. Only one of them should contain an intent filter with an action set to MAIN and a category of LAUNCHER. That activity will be the default activity.

**Directions**:

1. Create a new activity.
  - Click on File->New->Other
  - Select Android->Android Activity
  - Create a blank activity. The wizard will automatically create the activity, add it to AndroidManifest.xml, create a layout file, and create a menu file. If you want to delete an activity, you should remove the corresponding layout and menu file manually.
2. Modify the new activity's layout file so that you can recognize it as the second activity.
3. Modify AndroidManifest.xml to change the default activity.
4. Run the application and confirm that it starts with the second activity.


#### Snippets

    // Android Manifest.xml

    <activity
        android:name="codepath.apps.demointroandroid.SecondActivity"
        android:label="Second Activity" >
        <intent-filter>
            <action android:name="android.intent.action.MAIN" />
            <category android:name="android.intent.category.LAUNCHER" />
        </intent-filter>
    </activity>


### Exercise 2: Linear

**Goal**: Explore LinearLayout.

**Description**:

Layouts (ViewGroups) are containers for Views (e.g., TextViews, Buttons, etc) and may also contain other Layouts. Different layout types have different options for configuring how their contained Views are laid out.

The easiest to use and the most common Layout type is LinearLayout. LinearLayout either lays out its contained Views in a row or a column, depending on the orientation property.

Note: the gravity property specifies the alignment of the contained views (e.g., left, center, right, etc). This is different from layout_gravity, which specifies the alignment of the entire container with respect to its parent.

**Directions**:

1. Open the XML layout.
2. Change the root layout to be a LinearLayout.
3. Add the android:orientation property and set it to "vertical".
4. Add the android:gravity property and set it to "center".

#### Snippets

    <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:tools="http://schemas.android.com/tools"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:gravity="center"
        android:orientation="vertical" >

    </LinearLayout>


### Exercise 3: Layout Params

**Goal**: Explore layout widths.

**Description**:

There are 3 options for layout width: match_parent, wrap_content, and a dp value. match_parent sets the width to be the same width as the container. wrap_content will size the container to be just large enough to fit its content. A dp value will specify the exact width.

**Directions**:

1. Open the layout XML.
2. Add at least 3 TextViews to the vertical LinearLayout.
3. Set the android:background property to #00FF00, as below.
4. Set the first TextView width to be wrap_content.
5. Set the second TextView width to be match_parent.
6. Set the third TextView width to be 50dp.

#### Snippets

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:background="#00FF00"
        android:text="Wrap Content" />

    <TextView
         android:layout_width="match_parent"
         android:layout_height="wrap_content"
         android:background="#00FF00"
         android:text="Match Parent" />

    <TextView
         android:layout_width="50dp"
         android:layout_height="wrap_content"
         android:background="#00FF00"
         android:text="50dp" />
