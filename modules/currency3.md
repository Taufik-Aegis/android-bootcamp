
###### DevAcademy Android Bootcamp Notes

<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>

# App Project - Currency Converter - Phase 3

Adding capability to update currency rate from internet using `HttpURLConnection`, create new thread using `AsyncTask`, process JSON data, store currency data in `SharedPreferences`, and how to use permission.

## Networking

* Explain
  * Server - Client Architecture
  * Anatomy of HTTP request
  * HTTP request and response BODY
  * JSON

* Demo
  * In Chrome, install Postman
  * Make GET and POST request
  * Show network tab in Chrome developer window.

## Networking in Android


* Add Refresh button in Action Bar
  * res/menu/main.xml
  * Add refresh action
* Handle action in Activity. Remember Java `switch`

  ```
    public boolean onOptionsItemSelected(MenuItem item) {
      switch (item.getItemId()) {
      case R.id.action_refresh:
        // TODO : Check connection
        break;
      }
      return true;
    } 
  ```

* Check if we have connection

  ```
    ConnectivityManager connMgr = (ConnectivityManager) 
    getSystemService(Context.CONNECTIVITY_SERVICE);
    NetworkInfo networkInfo = connMgr.getActiveNetworkInfo();
    if (networkInfo != null && networkInfo.isConnected()) {
      String url = "https://openexchangerates.org/api/latest.json?app_id=cb0688771d774020836ec9422dfa93f7";
      downloadData(url);
    } else {
      Toast.makeText(getApplicationContext(), "Network connection is not available", Toast.LENGTH_SHORT).show();
    }
  ```

* Do actual download. Remember Java exception handling
  ```
    try
    {
       //Protected code
    }
    catch(Exception ex)
    {
       //Catch block
    }
    finally
    {
       //The finally block always executes.
    }
  ```

  ```
  private String downloadData(String url) {

    InputStream is = null;

    // create connection
    URL urlConn = new URL(url);
    HttpURLConnection conn = (HttpURLConnection) urlConn.openConnection();
    conn.setRequestMethod("GET");
    conn.setDoInput(true);
    
    // Starts the query
    conn.connect();
    
    // Get response
    int response = conn.getResponseCode();
    Log.d("NET", "The response is: " + response);
    is = conn.getInputStream();

    // Convert the InputStream into a string
    String contentAsString = "";
    BufferedReader buffer = new BufferedReader(new InputStreamReader(is));
    String s = "";
    while ((s = buffer.readLine()) != null) {
      contentAsString += s;
    }

    if (is != null) {
      is.close();
    }

    return contentAsString;
  }
  ```

* Try the app, what happened?
* Explain
  * permission

## Thread

* Use `AsyncTask`
* Declare private class

  ```
    private class DownloadCurrencyData extends AsyncTask<String, Void, String> {
      ...
    }
  ```

* Explain AsyncTask param
  * Params
  * Progress
  * Result

* Need to implements AsyncTask methods

  ```
    private class DownloadCurrencyData extends AsyncTask<String, Void, String> {
      
      // This runs in other thread
      @Override
      protected String doInBackground(String... params) {

        String url = params[0];

        try {
          // TODO 
          // Download currency data here
        } catch (IOException e) {
          return "Unable to retrieve web page. URL may be invalid.";
        }
      }

      // This runs in UI thread
      @Override
      protected void onPostExecute(String result) {
        // TODO
        // Parse JSON here
      }
    }
  ```

* Run `AsyncTask`

  ```
    String url = "https://openexchangerates.org/api/latest.json?app_id=cb0688771d774020836ec9422dfa93f7";
    new DownloadCurrencyData().execute(url);
  ```

* Task
  * Move our download code the AsyncTask

## Parsing JSON

* Use `JSONObject` and `JSONArray`
  ```
    JSONObject reader = new JSONObject(result);
    JSONObject rates  = reader.getJSONObject("rates");
    String base = reader.getString("base");
  ```

* Task
  * Parse JSON and update currency HashMap

## Storing data with SharedPreferences

* Write
    ```
    SharedPreferences sharedPref = getSharedPreferences("Currency", Context.MODE_PRIVATE);
    SharedPreferences.Editor editor = sharedPref.edit();
    editor.putString("latestCurrency", result);
    editor.commit();
    ```

* Read
    ```
    SharedPreferences sharedPref = getSharedPreferences("Currency", Context.MODE_PRIVATE);
    String latestCurrency = sharedPref.getString("latestCurrency", "");
    ```

* Task
  * Any idea?

## Intent

### Open browser

  ```
    Intent intent = new Intent(Intent.ACTION_VIEW, 
        Uri.parse("http://www.bloomberg.com/news/currencies/"));
    startActivity(intent);
  ```

### Share content

  ```
    Intent intent = new Intent(Intent.ACTION_SEND);
    intent.setType("text/plain");
    intent.putExtra(android.content.Intent.EXTRA_TEXT, "News for you!");
    startActivity(intent); 
  ```