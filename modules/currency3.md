
###### DevAcademy Android Bootcamp Notes

<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>

# App Project - Currency Converter - Phase 3

In phase 1, we have learn how to create a simple currency converter, we learn about a simple complete app, XML layout, string resource and create an event handler.

In phase 2, we have learn how to enhance currency converter app with multiple currencies capability. we learn how to use `Dialog` and use `Array` to store currency data.

In phase 3, we will learn new how to add new capability to our apps. We will add capability to update currency rate from internet using `HttpURLConnection`, create new thread using `AsyncTask`, process JSON data, store currency data in `SharedPreferences`, and how to use permission.

Using our previous layout we will add one new function/capability to our apps. Our apps now will get data of currency rates from internet using `HttpURLConnection`. First we create new component in our action bar.

## Add Refresh button in Action Bar

* Open `main.xml` file located in `Converter -> res -> menu` on Package Explorer.
* Click Add to create new menu element.
* Fill the id so we can referenced it later.
* Fill the title field using string resource like in previous phase.
* Fill the icon using drawable icon. First download the icon from here [<a href="http://developer.android.com/downloads/design/Android_Design_Downloads_20131106.zip" target="_blank">print</a>]
* Extract downloaded zip file and then copy refresh icon from the extracted zip file to it's respectable folder, `res -> drawable-xxxx`.

<img src="http://imageshack.com/a/img842/2392/31qu.png" alt="Create Refresh Action" />

## Handling Refresh button

After we create new button for our new function, next is create it's handler. We use `switch` function in `onOptionsItemSelected` method so that our handler will only running if button `Refresh` is clicked.

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

## Networking

We will use `ConnectivityManager` class to check if we have internet connection.

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
This url `https://openexchangerates.org/api/latest.json?app_id=cb0688771d774020836ec9422dfa93f7` will act as a request to get the latest currency rate from `openexchangerate.org`. This data provider will reply our request with sending data formatted in JSON.

## Download the data

To download the data we requested.

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
To implementing the `HttpURLConnection` class we must surround it with try catch block. So, if error arouse when app is running, it's exception class will handle it for us and the app wouldn't crash when running.

`HttpURLConnection` class using `GET` method to send it's request and response from data provider stored as a string.

## Thread

To make our app responsive, we use `AsyncTask` to running our downloading code so we can interact with our app even when our app is running code in the background.

* Use `AsyncTask`
* Declare private class

  ```
    private class DownloadCurrencyData extends AsyncTask<String, Void, String> {
      ...
    }
  ```

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
  * Move our download code to AsyncTask

With this code, our download code will running in the background process and will not hindered the flow of the app when refresh button is clicked.

## Parsing JSON

After we get the JSON data, next step is to parsing it. JSON object use some sort of structural data and to extract this JSON we need to follow this structure. We use `JSONObject` class to help us parsing our data.

* Use `JSONObject` and `JSONArray`
  ```
    JSONObject reader = new JSONObject(result);
    JSONObject rates  = reader.getJSONObject("rates");
    String base = reader.getString("base");
  ```

## Storing data with SharedPreferences

After we parsing JSON data, it's extracted data then stored in SharedPreferences.

* Write
    ```
    SharedPreferences sharedPref = getSharedPreferences("Currency", Context.MODE_PRIVATE);
    SharedPreferences.Editor editor = sharedPref.edit();
    editor.putString("latestCurrency", result);
    editor.commit();
    ```
To read the data that we stored in SharedPreferences we use this code.

* Read
    ```
    SharedPreferences sharedPref = getSharedPreferences("Currency", Context.MODE_PRIVATE);
    String latestCurrency = sharedPref.getString("latestCurrency", "");
    ```

This is a code that doing the download from data provider in `AsyncTask`, parsing it's response data that arrived and storing it's parsed data in SharedPreferences.

```
  private class DownloadCurrencyData extends AsyncTask<String, Void, String> {

    // fungsi dengan parameter, string... data berupa array
    @Override
    protected String doInBackground(String... params) {
      // TODO Auto-generated method stub

      // call url in background
      String url = params[0];
      String data = downloadData(url);
      // Log.v(TAG, data);

      return data;
    }

    // sebelum eksekusi
    @Override
    protected void onPreExecute() {
      // TODO Auto-generated method stub

    }

    // sesudah eksekusi
    @Override
    protected void onPostExecute(String result) {
      // TODO Auto-generated method stub
      // Log.v(TAG, result);

      Toast.makeText(getApplicationContext(),
          "Update nilai tukar terbaru", Toast.LENGTH_SHORT)
          .show();

      // { -> json as an object, [ -> json as an array
      try {
        JSONObject reader = new JSONObject(result);
        // Log.v(TAG, reader.getString("base"));

        JSONObject ratesData = reader.getJSONObject("rates");

        //store latest rate on file with sharedpreference
        SharedPreferences sharedPref = getSharedPreferences("Currency", Context.MODE_PRIVATE);
        SharedPreferences.Editor editor = sharedPref.edit();
        
        // get rates
        for (int i = 0; i < rates.length; i++) {

          Currency currency = rates[i];

          // update latest rate
          Double latestRate = ratesData.getDouble(currency.getName());
          Log.v(TAG, latestRate.toString());
          
          //save value
          editor.putString(currency.getName(), latestRate.toString());
          
          rates[i].setRate(latestRate);
        }
        
        editor.commit();

      } catch (Exception e) {
        // TODO: handle exception
        e.printStackTrace();
      }

    }

  }
```