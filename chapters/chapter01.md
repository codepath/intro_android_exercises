---
layout: exercises
title: Chapter 1
---

## Chapter 1 - App Fundamentals

### Exercise 1: Manifest

**Goal**: Explore the AndroidManifest file.

**Description**:

Every Android application has a file called AndroidManifest.xml that controls application-wide settings such as the display name, icon, theme, and default Activity.

**Directions**:

1. Open AndroidManifest.xml
   - Change the version code and name to 2 and 2.0. Reminder: version code is an integer value that you can programatically inspect in your application. Version name is displayed to the user.
   - Change the application name
   - Change the application icon
     - Find and download an image, e.g., from Google Images.
     - Create various resolution sizes for your image.
     - Tip: Use a tool to [automatically create the resolution sizes](http://android-ui-utils.googlecode.com/hg/asset-studio/dist/icons-launcher.html)
     - Place the various resolutions into the respective drawable folders.
     - In AndroidManifest.xml, point to the new drawable.


#### Snippets

    // AndroidManifest.xml
    <manifest xmlns:android="http://schemas.android.com/apk/res/android"
        package="codepath.apps.demointroandroid"
        android:versionCode="2"
        android:versionName="2.0" >

        <!-- More manifest text... -->

        <application
                android:allowBackup="true"
                android:icon="@drawable/ic_launcher"
                android:label="@string/app_name"
                android:theme="@style/AppTheme" >

        </application>

        <!-- More manifest text... -->
    </manifest>

### Exercise 2: TextView

**Goal**: Explore the XML layout of an Activity.

**Description**:

Every activity has an associated XML layout file specified in the onCreate method. The XML file is responsible for describing the elements (TextViews, Buttons, etc) that will be on the screen for that activity.

Every element has XML properties that describes various behavior such as layout, alignment, color, etc.

**Directions**:

1. Open the XML layout file (e.g., res/layout/activity_hello_world.xml)
2. Switch to the raw XML mode.
3. If there is not already a TextView in the layout, add one.
4. Modify the android:text property, as shown below.


#### Snippets

    <TextView
        android:text="Some New Text"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
    />

### Exercise 3: Strings

**Goal**: Modify strings in the strings.xml file.

**Description**:

The primary purpose of the strings.xml file is for internationalization. Any string that is ultimately shown to the user (e.g., in a text field, button, or navigation) should be added to the strings.xml file. That way, to add support for a new language simply requires adding an additional strings.xml file for the new language.

In XML, refer to strings described in the strings.xml file using the syntax @string/my_string.

**Directions**:

1. Open the XML layout file.
2. If you have any android:text values that do not refer to an @string, hover your mouse over the warning and read what it says.
3. Add new strings to the strings.xml file.  Note: the keys may not include spaces.
4. Modify all android:text properties to refer to a string


#### Snippets

    <TextView
        android:text="@string/second_textview"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
    />

### Exercise 4: Lifecycle

**Goal**: Explore the Activity lifecycle.

**Description**:

The Activity lifecycle is automatically managed by the Android framework. If a user taps on something that switches them into a new activity, the previous activity is paused. The activity is also paused if the user receives a phone call.

The 3 most commonly implemented activity lifecycle methods are onCreate, onPause, and onResume. Note: if you implement an activity lifecycle method, you MUST call the super implementation.

**Directions**:

1. Open the Activity java file (e.g., src/codepath/HelloWorldActivity.java)
2. Implement the onCreate, onPause, and onResume methods.
3. In each method, call the super method.
4. Add a Log.d message to each method, as shown below.
5. Run the application and observe the LogCat.
  - In the emulator, click the Home button.
  - Did you see the activity pause in the LogCat?


#### Snippets

    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_basic_text_view);
        Log.d("DEBUG", "onCreate was just called!");
    }

    protected void onResume() {
       super.onResume();
       Log.d("DEBUG", "onResume was just called!");
    }

    protected void onPause() {
       super.onPause();
       Log.d("DEBUG", "onPause was just called!");
    }

### Exercise 5: Size Units

**Goal**: Explore size units.

**Description**:

Android devices have a variety of screen resolutions. In other words, any given physical inch of the screen may contain 100 pixels, 200 pixels, or more, depending on the resolution. Therefore, if we specify measurements in pixels, the element (e.g., a TextView or Button) will appear to be different sizes on different devices.

Never use px for distance or pt for font size. Instead, use dp for distance and sp for font size.

**Directions**:

1. Open the layout XML.
2. For the TextView, add the property android:textSize and set it to 20sp.

#### Snippets

    <TextView
        android:textSize="20sp"
        android:text="@string/second_textview"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
     />