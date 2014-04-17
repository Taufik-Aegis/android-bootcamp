
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
* Fill the icon using drawable icon. First download the icon from here [<a href="http://developer.android.com/downloads/design/Android_Design_Downloads_20131106.zip" target="_blank">Download</a>]
* Extract downloaded zip file and then copy refresh icon from the extracted zip file to it's respectable folder, `res -> drawable-xxxx`.

<img src="http://imageshack.com/a/img842/2392/31qu.png" alt="Create Refresh Action" />

Button on action bar will show up in top region of our app, beside title app. We set this button to be visible and always show up.

## Handling Refresh button

After we create new button in action bar for our new function, next is create it's handler. We use `switch` function in `onOptionsItemSelected` method so that our handler will only running if action `Refresh` is clicked.

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

`onOptionsItemSelected` method is a handler for every action that created in `main.xml` file. This file contain every action button that we want to build. We have create action refresh button so we create a handler for it.

`onOptionsItemSelected` method received clicked action as it's parameter. This parameter and then passing to `switch` function to determined the right handler for this event. 

## Networking

We just create one handler for one event in our `switch` statement, it is an action refresh button handler.
To get data from the internet we need another class to help us. We will use `ConnectivityManager` class to check if we have internet connection. This class answers queries about the state of network connectivity. It also notifies applications when network connectivity changes.

The primary responsibilities of this class are to:

1. Monitor network connections (Wi-Fi, GPRS, UMTS, etc.).
2. Send broadcast intents when network connectivity changes.
3. Attempt to "fail over" to another network when connectivity to a network is lost.
4. Provide an API that allows applications to query the coarse-grained or fine-grained state of the available networks.

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

This url `https://openexchangerates.org/api/latest.json?app_id=cb0688771d774020836ec9422dfa93f7` is a request to get the latest currency rate from `openexchangerate.org`. This data provider will reply our request with sending data formatted in JSON.

JSON or JavaScript Object Notation, is an open standard format that uses human-readable text to transmit data objects consisting of attribute–value pairs. It is used primarily to transmit data between a server and web application, as an alternative to XML.

Although originally derived from the JavaScript scripting language, JSON is a language-independent data format, and code for parsing and generating JSON data is readily available in a large variety of programming languages.

The following example shows a possible JSON representation describing a person.
```
{
    "firstName": "John",
    "lastName": "Smith",
    "isAlive": true,
    "age": 25,
    "height_cm": 167.64,
    "address": {
        "streetAddress": "21 2nd Street",
        "city": "New York",
        "state": "NY",
        "postalCode": "10021-3100"
    },
    "phoneNumbers": [
        { "type": "home", "number": "212 555-1234" },
        { "type": "fax",  "number": "646 555-4567" }
    ]
}
```

If we success sending a request and `openexchangerate.org` accept our request and sending a JSON as a response, our data will be something like this.

```
{
  "disclaimer": "Exchange rates are provided for informational purposes only, and do not constitute financial advice of any kind. Although every attempt is made to ensure quality, NO guarantees are given whatsoever of accuracy, validity, availability, or fitness for any purpose - please use at your own risk. All usage is subject to your acceptance of the Terms and Conditions of Service, available at: https://openexchangerates.org/terms/",
  "license": "Data sourced from various providers with public-facing APIs; copyright may apply; resale is prohibited; no warranties given of any kind. Bitcoin data provided by http://coindesk.com. All usage is subject to your acceptance of the License Agreement available at: https://openexchangerates.org/license/",
  "timestamp": 1397703644,
  "base": "USD",
  "rates": {
    "AED": 3.673076,
    "AFN": 56.7753,
    "ALL": 101.404659,
    "AMD": 416.860998,
    "ANG": 1.7855,
    "AOA": 97.796775,
    "ARS": 8.000922,
    "AUD": 1.066523,
    "AWG": 1.7825,
    "AZN": 0.783933,
    "BAM": 1.414489,
    "BBD": 2,
    "BDT": 77.65953,
    "BGN": 1.414612,
    "BHD": 0.377024,
    "BIF": 1543.0833,
    "BMD": 1,
    "BND": 1.251159,
    "BOB": 6.912136,
    "BRL": 2.239799,
    "BSD": 1,
    "BTC": 0.0019389239,
    "BTN": 60.343263,
    "BWP": 8.755123,
    "BYR": 9958.015,
    "BZD": 2.01522,
    "CAD": 1.100114,
    "CDF": 920.178,
    "CHF": 0.88025,
    "CLF": 0.02348,
    "CLP": 556.192899,
    "CNY": 6.212072,
    "COP": 1927.926667,
    "CRC": 548.2619,
    "CUP": 1.000375,
    "CVE": 79.43658,
    "CZK": 19.85279,
    "DJF": 179.342299,
    "DKK": 5.396497,
    "DOP": 43.01381,
    "DZD": 78.77706,
    "EEK": 11.6266,
    "EGP": 6.984551,
    "ERN": 14.9524,
    "ETB": 19.44757,
    "EUR": 0.722597,
    "FJD": 1.83523,
    "FKP": 0.59409,
    "GBP": 0.59409,
    "GEL": 1.75808,
    "GHS": 2.779356,
    "GIP": 0.59409,
    "GMD": 39.60444,
    "GNF": 6958.196667,
    "GTQ": 7.756653,
    "GYD": 204.351249,
    "HKD": 7.754425,
    "HNL": 19.1268,
    "HRK": 5.510147,
    "HTG": 44.65378,
    "HUF": 222.783499,
    "IDR": 11446.133333,
    "ILS": 3.47534,
    "INR": 60.32657,
    "IQD": 1164.235,
    "IRR": 25315.666667,
    "ISK": 111.921999,
    "JEP": 0.59409,
    "JMD": 109.5912,
    "JOD": 0.707698,
    "JPY": 101.9883,
    "KES": 86.864729,
    "KGS": 54.41845,
    "KHR": 4004.718333,
    "KMF": 355.939177,
    "KPW": 900,
    "KRW": 1038.236659,
    "KWD": 0.281489,
    "KYD": 0.82653,
    "KZT": 182.056799,
    "LAK": 8037.726667,
    "LBP": 1509.455,
    "LKR": 130.576299,
    "LRD": 85.5,
    "LSL": 10.54746,
    "LTL": 2.496561,
    "LVL": 0.508235,
    "LYD": 1.238848,
    "MAD": 8.12118,
    "MDL": 13.41685,
    "MGA": 2363.908333,
    "MKD": 44.58751,
    "MMK": 961.0944,
    "MNT": 1769.5,
    "MOP": 7.987716,
    "MRO": 296.7009,
    "MTL": 0.683738,
    "MUR": 30.15442,
    "MVR": 15.42409,
    "MWK": 392.4534,
    "MXN": 13.06202,
    "MYR": 3.240083,
    "MZN": 31.045375,
    "NAD": 10.54626,
    "NGN": 162.057601,
    "NIO": 25.74532,
    "NOK": 5.969834,
    "NPR": 96.660401,
    "NZD": 1.158277,
    "OMR": 0.385007,
    "PAB": 1,
    "PEN": 2.779188,
    "PGK": 2.747112,
    "PHP": 44.44665,
    "PKR": 96.408049,
    "PLN": 3.028014,
    "PYG": 4427.698359,
    "QAR": 3.640867,
    "RON": 3.229085,
    "RSD": 83.51968,
    "RUB": 36.02236,
    "RWF": 679.7252,
    "SAR": 3.750232,
    "SBD": 7.269808,
    "SCR": 12.14345,
    "SDG": 5.688505,
    "SEK": 6.585676,
    "SGD": 1.250585,
    "SHP": 0.59409,
    "SLL": 4336,
    "SOS": 978.2603,
    "SRD": 3.263333,
    "STD": 17729.816667,
    "SVC": 8.749125,
    "SYP": 145.965027,
    "SZL": 10.55194,
    "THB": 32.22205,
    "TJS": 4.828,
    "TMT": 2.8501,
    "TND": 1.585049,
    "TOP": 1.820333,
    "TRY": 2.136869,
    "TTD": 6.460389,
    "TWD": 30.14725,
    "TZS": 1632.668333,
    "UAH": 12.59859,
    "UGX": 2512.456667,
    "USD": 1,
    "UYU": 22.84803,
    "UZS": 2274.680007,
    "VEF": 6.291481,
    "VND": 21089.766667,
    "VUV": 94.5725,
    "WST": 2.293621,
    "XAF": 474.58252,
    "XAG": 0.05102733,
    "XAU": 0.0007683,
    "XCD": 2.70156,
    "XDR": 0.644999,
    "XOF": 474.9082,
    "XPF": 86.367889,
    "YER": 214.927899,
    "ZAR": 10.5477,
    "ZMK": 5253.075255,
    "ZMW": 6.238483,
    "ZWL": 322.355006
  }
}
```

## Download the data

This is a piece of code that download the data. We surround this code using java exception handling.

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

An exception is a problem that arises during the execution of a program. An exception can occur for many different reasons, including the following:

* A user has entered invalid data.

* A file that needs to be opened cannot be found.

* A network connection has been lost in the middle of communications or the JVM has run out of memory.

Some of these exceptions are caused by user error, others by programmer error, and others by physical resources that have failed in some manner.

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
To implementing the `HttpURLConnection` class we must surround it with try, catch, finally block. So, if error arise when app is running, it's exception class will handle it for us and the app wouldn't crash when running.

This code tell the app to create a connection. But to create a success connection our app must be allowed to use the connection service in our device so we must set the permission to allowing the app to use the connection.

Type this code in `onCreate` method. This code will set our app to be allowed using any available service in our device.

```
    StrictMode.ThreadPolicy policy = new StrictMode.ThreadPolicy.Builder()
    .permitAll().build();
    StrictMode.setThreadPolicy(policy);
``` 

`HttpURLConnection` class using `GET` method to send it's request (url parameter that we passing) and a response data sent from our data provider will be stored as a string. This string contain data formatted as a JSON. Later we must parsing it before we use it in our app.

## Thread

Create a connection and downloading data from internet takes time. We wouldn't want to make our app freezing waiting the data to be completely downloaded. In serial programming, one statement executed one at a time. Next statement will not executed until previous statement is completed. If we not use `AsyncTask` our app will freeze for a second right after we click refresh action an will unfreeze until the data that we requested arrived completely. To handle this situation we will use `AsyncTask`. `AsyncTask` will offloaded our download code in separate thread aside from our main thread so we can interact with our app even when our app is downloading the data in the background.

AsyncTask enables proper and easy use of the UI thread. This class allows to perform background operations and publish results on the UI thread without having to manipulate threads and/or handlers.

AsyncTask is designed to be a helper class around Thread and Handler and does not constitute a generic threading framework. AsyncTasks should ideally be used for short operations (a few seconds at the most.) If you need to keep threads running for long periods of time, it is highly recommended you use the various APIs provided by the java.util.concurrent package such as Executor, ThreadPoolExecutor and FutureTask.

An asynchronous task is defined by a computation that runs on a background thread and whose result is published on the UI thread. An asynchronous task is defined by 3 generic types, called Params, Progress and Result, and 4 steps, called onPreExecute, doInBackground, onProgressUpdate and onPostExecute.

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

SharedPreferences is an interface for accessing and modifying preference data returned by getSharedPreferences(String, int). For any particular set of preferences, there is a single instance of this class that all clients share. Modifications to the preferences must go through an SharedPreferences.Editor object to ensure the preference values remain in a consistent state and control when they are committed to storage. Objects that are returned from the various get methods must be treated as immutable by the application. 

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

This is a complete code `DownloadCurrencyData` that doing the download from data provider in `AsyncTask`, parsing it's response data that arrived and storing it's parsed data in SharedPreferences.

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