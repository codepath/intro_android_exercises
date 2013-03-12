---
layout: exercises
title: Chapter 7
---

## Chapter 7 - Advanced Views

### Exercise 1: Toast Inputs

**Goal**: Experiment with three basic input views: EditText, CheckBox, and RadioGroup.

**Description**:

This is a basic exercise in the usage of a few common input views.

**Directions**:

1. Create a new Activity with an EditText, a CheckBox, and a RadioGroup.
2. In the onCreate method, find and store each view into an instance variable.
3. Add a button to the activity and implement a click handler.
   - In the click handler, display a Toast of the current values of the EditText, CheckBox, and RadioGroup.

#### Snippets

    @Override
    protected void onCreate(Bundle savedInstanceState) {
      // ...
      etVal = (EditText) findViewById(R.id.etVal);
      chkVal = (CheckBox) findViewById(R.id.chkVal);
      rdgVal = (RadioGroup) findViewById(R.id.rdgVal);
    }

    public void toastInputs(View v) {
      int selected = rdgVal.getCheckedRadioButtonId();
      RadioButton b = (RadioButton) findViewById(selected);

      String text = etVal.getText() + " | " + chkVal.isChecked() + " | " + b.getText();
      Toast.makeText(this, text, Toast.LENGTH_SHORT).show();
    }


### Exercise 2: Spinner Toast

**Goal**: Use a Spinner to select one of a few choices.

**Description**:

A spinner is a control used by things like alarm clocks. Upon clicking a Spinner, it will display a pull down menu of different options to choose between.

Similar to ListView, Spinner is also an adapter view. In other words, it displays the data that it finds in its attached adapter. There are many ways to create adapters that a Spinner can use. In this exercise, we will use an ArrayAdapter that is initialized using an XML string array.

Like a ListView, each item in a Spinner can be rendered using a custom view. In this exercise, we will use a built-in view called `android.R.layout.simple_spinner_item`.

**Directions**:

1. Create an XML file called spinner_values.xml in res/values
2. Create a new Activity that includes a Spinner.
3. In the onCreate method
   - Create an ArrayAdapter with the XML array and a default spinner layout.
   - Set the dropDownViewResource to a default dropdown layout.
   - Set the adapter on the spinner to the newly created ArrayAdapter.
4. Add a button to the activity. In the click handler,
   - Fetch the current value of the Spinner and display a Toast of the current value

#### Snippets

    // res/values/spinner_values.xml
    <?xml version="1.0" encoding="utf-8"?>
    <resources>
        <string-array name="spinner_options">
           <item>Red</item>
           <item>Orange</item>
           <item>Yellow</item>
           <item>Green</item>
           <item>Blue</item>
           <item>Indigo</item>
           <item>Violet</item>
        </string-array>
    </resources>

    // In Java Activity
    private void loadSpinner() {
      ArrayAdapter<CharSequence> adapter = ArrayAdapter.createFromResource(this,
        R.array.spinner_options, android.R.layout.simple_spinner_item);
      // Set layout style during dropdown
      adapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
      // Load data from adapter
      spinner.setAdapter(adapter);
    }


### Exercise 3: Time Picker

**Goal**: Explore using a TimePicker view.

**Description**:

This is a basic exercise using the TimePicker view.

**Directions**:

1. Create an Activity with a TimePicker view.
2. Add a button. In the click handler,
   - Display a toast of the current selected time.


#### Snippets

    // Java Activity
    public void displayTime(View v) {
      String time = tpTime.getCurrentHour() + ":" + tpTime.getCurrentMinute();
      Toast.makeText(this, time, Toast.LENGTH_SHORT).show();
    }

### Exercise 4: ProgressBar

**Goal**: Create a ProgressBar that reflects the progress of some network requests.

**Description**:

In this exercise, we will leverage some additional features of the AsyncTask class, notably the ability to report incremental progress. This involves calling the method publishProgress in the doInBackground() method, which triggers a call to onProgressUpdate() method. The reason it must be done like this is that UI updates may not be done in the background thread. The onProgressUpdate() method is called in the main thread.

**Directions**:

1. Create a new Activity with a horizontal ProgressBar, a TextView, and a Submit button.
2. Create an `ArrayList<String>` to store the first line of each network response.
3. Implement a private, inner class called DelayTask.
   - In `onPreExecute`, show the hidden ProgressBar.
   - In `doInBackground`, download the 4 sites and call publishProgress after each site completes its download.
   - In `onProgressUpdate`, update the ProgressBar.
   - In `onPostExecute`, update the TextView with the downloaded responses.

#### Snippets

    ProgressBar pb;
    TextView tvResult;
    ArrayList<String> lines = new ArrayList<String>();

    public void startFourUrlAsync(View v) {
         new DelayTask().execute();
    }

    public class DelayTask extends AsyncTask<Void, Integer, String> {
      int count = 0;
      @Override
      protected void onPreExecute() {
        pb.setVisibility(ProgressBar.VISIBLE);
      }

      @Override
      protected String doInBackground(Void... params) {
        String res = loadUrlBody("http://google.com");
        lines.add(res.split("\n")[0]);
        publishProgress(25.;
        res = loadUrlBody("http://yahoo.com");
        lines.add(res.split("\n")[0]);
        publishProgress(50.;
        res = loadUrlBody("http://twitter.com");
        lines.add(res.split("\n")[0]);
        publishProgress(75.;
        res = loadUrlBody("http://facebook.com");
        lines.add(res.split("\n")[0]);
        publishProgress(100.;
        return "complete";
      }

      @Override
      protected void onProgressUpdate(Integer... values) {
         pb.setProgress(values[0]);
      }

      @Override
      protected void onPostExecute(String result) {
        Toast.makeText(ProgressBarActivity.this, "Completed!", Toast.LENGTH_SHORT).show();
        tvResult.setText(lines.toString());
      }

      protected String loadUrlBody(String address) {
        HttpClient httpclient = new DefaultHttpClient();
        HttpResponse response = null;
        String responseString = null;
        try {
          response = httpclient.execute(new HttpGet(address));
          StatusLine statusLine = response.getStatusLine();
            if(statusLine.getStatusCode() == HttpStatus.SC_OK){
                ByteArrayOutputStream out = new ByteArrayOutputStream();
                response.getEntity().writeTo(out);
                out.close();
                responseString = out.toString();
            } else{
                response.getEntity().getContent().close();
                throw new IOException(statusLine.getReasonPhrase());
            }
        } catch (ClientProtocolException e) {
          // nothing
        } catch (IOException e){
          // nothing
        }
        return responseString;
      }

    }

### Exercise 5: GridView

**Goal**: Create a GridView to display 6 images.

**Description**:

Like ListView and Spinner, GridView is an adapter view. In other words, it displays the data that it finds in its attached adapter. In this exercise, we will display 6 images in a grid using a GridView.

Adapters can specify an XML file to display each item. However, to customize the view, one must subclass the ArrayAdapter class and override the getView method.

**Directions**:

1. Create a new Activity with a GridView that fills the entire screen.
2. Download and copy 6 images into the drawables folder. You only need to copy the images into one of the drawables folders.
3. Create a new class called GridImageAdapter that is a subclass of ArrayAdapter.
   - Override the getView method to create a custom view.
   - Set the appropriate image based on the index.
4. In the onCreate method, create a GridImageAdapter and set it to the GridView.


#### Snippets

    GridView gvImages;
    GridImageAdapter adapter;

    protected void loadGridViewImages() {
        gvImages = (GridView) findViewById(R.id.gvImages);
        String[] numbers = new String[] { "ad", "ae", "af", "ag", "ai", "al"};
        adapter = new GridImageAdapter(this,
            android.R.layout.simple_list_item_1, numbers);
        gvImages.setAdapter(adapter);
    }

    class GridImageAdapter extends ArrayAdapter<String> {

      public GridImageAdapter(Context context, int textViewResourceId, String[] numbers) {
        super(context, textViewResourceId, numbers);
      }

      public View getView(int position, View convertView, ViewGroup parent) {
          ImageView v = new ImageView(GridViewDemoActivity.this);
          int resId = getResources().getIdentifier(getItem(position), "drawable", getPackageName());
          v.setImageDrawable(getResources().getDrawable(resId));
          return v;
      }

    }