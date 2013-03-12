---
layout: exercises
title: Chapter 6
---

## Chapter 6 - Networking

### Exercise 1: Image Download

**Goal**: Download an image.

**Description**:

When making network requests, there are a couple of requirements: permissions and threading.

Android requires an application to request permissions for certain things, such as accessing the internet, the call log, the contact book, etc. Permissions are requested by listing them in AndroidManifest.xml.

Android is mostly single threaded. This is by design because it is easy to introduce undesirable behavior with multiple threads. However, accessing the network or the disk in the main thread will cause the main thread to be unresponsive to user interaction. Android added a concept called StrictMode that enforces the rule that network requests must never be made on the main thread. In the next lesson, we will learn how to move the network request to a background thread. For now, we will disable the StrictMode rule and download the image in the main thread.

**Directions**:

1. Modify AndroidManifest.xml to request the INTERNET permission.
2. Create a new Activity with an ImageView.
3. In the onCreate,
   - Disable StrictMode for network access.
   - Call a method, downloadImageFromUri(String address)
4. Implement downloadImageFromUri(String address)
   - Create the URL from the string.
   - Open a URLConnection.
   - Get an InputStream from the connection.
   - Decode the image using the BitmapFactory.
   - Set the bitmap of the ImageView.

#### Snippets

    // Manifest
    <uses-permission android:name="android.permission.INTERNET" />

    // In Activity

    @Override
    protected void onCreate(Bundle savedInstanceState) {
      // ...
      StrictMode.setThreadPolicy(
            new StrictMode.ThreadPolicy.Builder().permitNetwork().build());
      downloadImageFromUri("http://...some/image/url");
    }


    private void downloadImageFromUri(String address) {
      URL url;
      try {
        url = new URL(address);
      } catch (MalformedURLException e1. {
        url = null;
      }

      URLConnection conn;
      InputStream in;
      Bitmap bitmap;
      try {
        conn = url.openConnection();
        conn.connect();
        in = conn.getInputStream();
        bitmap = BitmapFactory.decodeStream(in);
        in.close();
      } catch (IOException e) {
        bitmap = null;
      }

      if (bitmap != null) {
        ImageView img = (ImageView) findViewById(R.id.ivBasicImage);
        img.setImageBitmap(bitmap);
      }
    }


### Exercise 2: AsyncTask

**Goal**: Background a task using AsyncTasks.

**Description**:

For the most part, application code should run in the primary thread for simplicity. However, slow tasks such network access or disk access should be run in a background thread.

Android provides the AsyncTask class which handles much of the complexity of creating and managing threads. In the Activity that has a task to be backgrounded, implement one or more subclasses of AsyncTask as a private, inner class. AsyncTask is a generic class, whose parameters are the input type, output type, and metric for tracking progress. In this example, we will implement an AsyncTask that has no input and output, so those parameters will be Void.

An AsyncTask has a few methods, but the most commonly implemented are the doInBackground() and onPostExecute() methods. Any code that is in the doInBackground() method is automatically run in the background thread. Upon completion of the doInBackground method(), the AsyncTask will call the onPostExecute() method and run it in the main thread. This is useful because all UI methods MUST be run in the main thread or the application will crash.

In this exercise, we will simply count to 100,000 and display a Toast message when we're done counting.

**Directions**:

1. In the default Activity, implement `MyAsyncTask` as a subclass of `AsyncTask<Void, Void, Void>`
   - In doInBackground, print out the numbers 0 to 100,000.
   - In onPostExecute, display a Toast message.
2. In the onCreate method, instantiate an object of MyAsyncTask and call the execute() method.
3. Run the application and note that the Toast message will appear after some delay. If there is not a noticeable delay, increase the counter to 1,000,000 or more.


#### Snippets

    // In Activity
    @Override
    protected void onCreate(Bundle savedInstanceState) {
       // ...
       new MyAsyncTask().execute();
    }

    public void doneCounting() {
      Toast.makeText(this, "Done Counting to 100000", Toast.LENGTH_SHORT).show();
    }

    private class MyAsyncTask extends AsyncTask<Void, Void, Void> {
        public Void doInBackground(Void... params) {
          for (long i=0; i < 100000; i++) {
            System.out.println(i);
          }
          return null;
        }

        protected void onPostExecute(Void result) {
          doneCounting();
        }
    }

### Exercise 3: AsyncHTTPClient

**Goal**: Download an image asynchronously.

**Description**:

Using the built-in URLConnection class and AsyncTasks, it's possible to download images from the internet asynchronously. However, third party libraries exist to provide this functionality in a more convenient way. A popular third party library is AsyncHttpClient, which makes all its network requests asynchronously.

This library uses anonymous classes to receive the desired method from the developer.

**Directions**:

1. Create an Activity with an ImageView.
2. Find the URL of an image to test.
3. In the onCreate method, call downloadImageFromUrl(String address)
4. Implement downloadImageFromUrl(String address) like the snippet below

Reference:

Download the library from: http://loopj.com/android-async-http/


#### Snippets

    // In Java
    private void downloadImageFromUrl(String address) {
      AsyncHttpClient client = new AsyncHttpClient();
      client.get(address, new
          BinaryHttpResponseHandler() {
              @Override
              public void onSuccess(byte[] image) {
                Bitmap bitmap = BitmapFactory.decodeByteArray(image, 0, image.length);
                ImageView img = (ImageView) findViewById(R.id.ivSmartImage);
                img.setImageBitmap(bitmap);
              }
          }
      );
    }