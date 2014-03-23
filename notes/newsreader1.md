
# News Reader phase 1

## API

* Explain API
  * Login
  * News list
  * News content
* Test on Postman

## UI and components

* Explain UI flow
  * Login
  * News list
  * News content

* Explain components
  * SQLite
  * Preferences
  * HTTP Post request

## Create Android App

* Explained in [helloworld](helloworld.md)

## Create login activity

* File -> New -> Other -> Android Activity
* Blank Activity. Next.
* Set activity name: LoginActivity. Next.
* See what changes to be performed. Finish

## Edit login layout

* res/layout/activity_login.xml
* Add View
  * TextView 
  * Edit Text for username
  * Edit Text for password
  * Button
* Set id and text for each view
* Add onClick handler for button

## Edit LoginActivity class

* add onClick handler

  ```
    public void loginButtonClicked(View view) {
      // TODO 
      // use findViewById() to get username and password text
      
      // Check connection
      // If OK, do login in background. Why?
    }
  ```

* Create Login AsyncTask

  ```
    private class LoginConnection extends AsyncTask<String, Void, String> {
      
      // This runs in other thread
      @Override
      protected String doInBackground(String... params) {

        try {
          // TODO 
          // Login code here
        } catch (IOException e) {
          return "Unable to retrieve web page. URL may be invalid.";
        }
      }

      // This runs in UI thread
      @Override
      protected void onPostExecute(String result) {
        // TODO
        // Parse JSON here
        // Store Login data in SharedPreferences
      }
    }
  ```

* HTTP POST. Remember HTTP GET

  ```
  ...
    // Create JSON string from login data
    JSONObject loginData = new JSONObject();
    loginData.put("name", name);
    loginData.put("pass", password);
    Log.d(TAG, "The body is: " + loginData.toString());
    
    // Open connection
    URL urlConn = new URL(url);
    HttpURLConnection conn = (HttpURLConnection) urlConn.openConnection();
    
    // Set header
    conn.setRequestProperty("Content-Type", "application/json");
    conn.setRequestMethod("POST");
    conn.connect();
    
    // Add POST body
    byte[] outputBytes = loginData.toString().getBytes("UTF-8");
    OutputStream os = conn.getOutputStream();
    os.write(outputBytes);
    os.close();
    
    // Get response
    int response = conn.getResponseCode();
    Log.d(TAG, "The response is: " + response);
    
    // Get data
    is = conn.getInputStream();
  ...
  ```

* Then what? Any idea?
* Explain
  * Android navigation
  * Use `finish()` to remove Activity from stack
* Question
  * Why we are not using login activity as main in manifest?
* Tasks
  * Store login information into SharedPreferences
  * Check if user is logged in MainActivity class. If not, open LoginActivity using intent

  ```
    Intent i = new Intent(getApplicationContext(), LoginActivity.class);
    startActivity(i);
    finish();
  ```
