---
layout: exercises
title: Chapter 4
---

## Chapter 4 - Interactions

### Exercise 1: Click Handlers

**Goal**: Add a click handler to a button.

**Description**:

Click handlers are methods that will be called when a button is called. Click handlers can be registered either in the XML or in Java. Whenever possible, add the click handler in XML. However, in some situations, such as dynamically created buttons, the click handler must be registered in Java using anonymous classes.

**Directions**:

1. Create a view that has two buttons.
2. For the first button,
   - Add the android:onClick property as in the snippet below, and set it to "firstButtonClicked"
   - Add the method "void firstButtonClicked(View view)"
   - Log the button click.
3. For the second button,
   - In the onCreate method of the activity, get a handle to the second button using findViewById, and set the OnClickListener.
   - Log the button click.


#### Snippets

    // First button with xml onClick
    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="20dp"
        android:onClick="firstButtonClicked"
        android:text="XML onClick" />


    // Java Activity
    protected void onCreate(Bundle savedInstanceState) {
        // ...
      Button secondButton = (Button) findViewById(R.id.btnClick2.;
      secondButton.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View v) {
          secondButtonClicked(v);
        }
      });
    }

    public void firstButtonClicked(View v) {
      // ...
    }


    public void secondButtonClicked(View v) {
      // ...
    }


### Exercise 2: Toast

**Goal**: To display a toast message.

**Description**:

A toast is a text view that appears in the bottom half of the screen that automatically fades away after a short delay. It is used to display transient messages.

**Directions**:

1. In the onClick method of a button, display a message using a Toast.


#### Snippets

    // Use Toast to show message in methods
    Toast.makeText(MyActivityClass.this, "firstButton clicked via XML handler", Toast.LENGTH_SHORT).show();

### Exercise 3: ListView Clicks

**Goal**: Implement handling a click on a row in a ListView.

**Description**:

ListViews display a collection of data, which it accesses via an Adapter. Each item in the collection can be rendered in a custom view. In this exercise, we will create a simple ListView with a default view and handle clicks on a row.

**Directions**:

1. In a new Activity, create a ListView that fills the screen.
2. In the onCreate method of the Activity
   - Create a string Array of countries.
   - Instantiate an array adapter with the string array and a default XML layout, android.R.layout.simple_list_item_1.
   - Set the adapter of the ListView to the array adapter.
   - Set the onItemClickListener of the ListView to display a toast upon clicking on the row.
     The toast should indicate which country was selected.


#### Snippets

    String[] myCountries = { "United States", "Canada", "Mexico", "Japan" };
    adapter = new ArrayAdapter<String>(this,
      android.R.layout.simple_list_item_1, myCountries);

    ListView listView = (ListView) findViewById(R.id.lvDemo);
    listView.setAdapter(adapter);

    listView.setOnItemClickListener(new OnItemClickListener() {
      @Override
      public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
        String country = adapter.getItem(position);
        Toast.makeText(ListViewClicksActivity.this, country, Toast.LENGTH_SHORT).show();
      }

    });