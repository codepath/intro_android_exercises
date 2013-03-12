---
layout: exercises
title: Chapter 5
---

## Chapter 5 - User Flows

### Exercise 1: Explicit Intents

**Goal**: Launch other activities in the application via explicit intents.

**Description**:

An explicit intent is how to launch one Activity in an application from another Activity in the same application. The intent's primary role is to specify which Activity class is to be launched. However, it can also pass along data which the new Activity can read.

All activities are associated with an originating intent. Retrieve the originating intent at any time using the method getIntent().

**Directions**:

1. Add a button to the default activity and label it "Launch".
2. Register a click handler via XML or Java
3. In the click handler method,
   - Create an intent, initializing it with the Activity to be launched.
   - Put a string "extra" in the intent.
   - Start the second activity.
4. In the second Activity,
   - Get the originating intent using getIntent()
   - Get the string "extra" from the intent.
   - Set the text of a TextView to the string "extra".


#### Snippets

    // In Activity
    Button btnLaunchSecond = (Button) findViewById(R.id.btnLaunchSecond);
    btnLaunchSecond.setOnClickListener(new OnClickListener() {
      @Override
      public void onClick(View v) {
        Intent i = new Intent(this, SimpleBundleDemoActivity.class);
        i.putExtra("text", "Passed String Extra!");
        startActivity(i);
      }
    });

    // In Launched Activity
    String initialText = getIntent().getStringExtra("text");
    TextView tvDisplayText = (TextView) findViewById(R.id.tvDisplayText);
    tvDisplayText.setText(initialText);


### Exercise 2: Implicit Intents

**Goal**: Launch a browser using implicit intents.

**Description**:

When launching another activity in the same application, use explicit intents to designate the activity to launch. However, in order to launch other applications, one must use implicit intents which does not specify a specific activity. An implicit intent uses a combination of an action, data, and a category to determine which application to launch. In some cases, more than one application may have an "intent filter" that matches the criteria of the implicit intent.

Although there are many rules to matching implicit intents with intent filters, the most common implicit intents specify and action (e.g., ACTION_VIEW) and data with a URL, like http:// or loc:// or contacts://. Android uses the protocol, e.g., http, to match with the appropriate application, like the browser, maps, calendar, contacts, phone, etc.

**Directions**:

1. In a new activity, add an EditText and Button view.
2. In the button click handler,
   - Create a Uri based on the text in the EditText field.
   - Create an intent w/ the ACTION_VIEW action and the url data.
   - Start an activity with the implicit intent.


#### Snippets

    // In Java Activity
    public void visitUrlAddress(View v) {
      Uri url = getUriToVisit();
      if (url != null) {
        Intent i = new Intent(Intent.ACTION_VIEW);
        i.setData(url);
        startActivity(i);
      }

    }

    public Uri getUriToVisit() {
      String urlAddress =  ((TextView) findViewById(R.id.txtUrlAddress)).getText().toString();
      if (urlAddress != null) {
        if (!urlAddress.startsWith("http://"))
           urlAddress = "http://" + urlAddress;
        return Uri.parse(urlAddress);
      } else {
        return null;
      }
    }

### Exercise 3: Intents With Results

**Goal**: Use an intent that passes back a result.

**Description**:

Sometimes, when launching an activity, it's convenient to give the originating activity some result. An example of this use case is when the launched activity is gathering some information from the user in a form.

**Directions**:

1. In a new Activity,
   - Add a TextView and a Button.
   - In the button click handler, launch another activity using startActivityForResult
   - Override onActivityResults
     - Set the text of the TextView to the returned data.
2. In the second Activity,
   - Create an EditText and a Button
   - In the button click handler,
     - Create an intent and add string extra into it.
     - Call setResult(RESUILT_OK, intent)
     - Call finish() to dismiss the current Activity


#### Snippets

    // In Activity
    final static int GET_RESULT_TEXT = 0;

    public void enterText(View v) {
      startActivityForResult(
            new Intent(IntentWithResultActivity.this, SimpleReturnResultActivity.class),
              GET_RESULT_TEXT);
    }

    // Handle the result once the activity returns a result, display contact
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
      if (requestCode == 0. {
        if (resultCode == RESULT_OK) {
          TextView tvResult = (TextView)findViewById(R.id.txtDisplayResult);
          tvResult.setText(data.getStringExtra("result"));
          Toast.makeText(this, data.getStringExtra("result"), Toast.LENGTH_SHORT).show();
        }
      }
    }

    // Returning Activity
    public void sendResult(View v) {
      String result = ((EditText) findViewById(R.id.txtRandomResultText)).getText().toString();
      Intent i = new Intent();
      i.putExtra("result", result);
      setResult(RESULT_OK, i);
      finish();
    }

### Exercise 4: Action Bar

**Goal**: Build an action bar with 2 icons.

**Description**:

Google is encouraging application developers to adopt the action bar, which is a title bar at the top of the screen with buttons. This is meant to be a replacement for the context menu used in early versions of Android.

In this exercise, we will add 2 action buttons. One will simply display a Toast and the other will launch another Activity.

**Directions**:

1. Open the menu XML for the default Activity (e.g., res/menu/my_activity.xml). Note that this different than the layout XML.
2. Add 2 menu items, as shown in the snippet below.
3. Override the onOptionsItemSelected method in the Activity.
   - Add a switch statement for the MenuItem.
   - Either create a Toast for launch the next activity.


#### Snippets

    // res/menu/my_activity.xml
    <menu xmlns:android="http://schemas.android.com/apk/res/android" >
        <item
          android:id="@+id/menu_toast"
          android:icon="@drawable/some_toast_icon"
          android:showAsAction="ifRoom|withText"
          android:title="Toast" />

        <item
          android:id="@+id/menu_launch"
          android:icon="@drawable/some_launch_icon"
          android:showAsAction="ifRoom|withText"
          android:title="Second" />
    </menu>

    // In Java Activity
    @Override
    public boolean onOptionsItemSelected(MenuItem item) {
      switch (item.getItemId()) {
      case R.id.menu_toast:
        Toast.makeText(this, "Toasted", Toast.LENGTH_SHORT).show();
        break;
      case R.id.menu_launch:
        Intent i = new Intent(this, SimpleBundleDemoActivity.class);
        startActivity(i);
        break;
      default:
        break;
      }
      return true;
    }