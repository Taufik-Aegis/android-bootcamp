
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

# News Reader phase 2

## Get news list

* In MainActivity.java
* Add refreshNewsList function

  ```
    private class refreshNewsList(String token) {
      // TODO 
      // Check if network connected
      // If connected get news list using AsyncTask
    }
  ```
* Add AsyncTask

  ```
    private class NewsListConnection extends AsyncTask<String, Void, String> {
      
      // This runs in other thread
      @Override
      protected String doInBackground(String... params) {

        try {
          // TODO 
          // Get news code here
          // Parse JSON here
          // Store News in SQLite here
        } catch (IOException e) {
          return "Unable to retrieve web page. URL may be invalid.";
        }
      }

      // This runs in UI thread
      @Override
      protected void onPostExecute(String result) {
        // TODO
        // Update UI here
      }
    }
  ```

## Add refresh action and loading icon

### Refresh action bar

* res/menu/main.xml
* Add new action
  * Create new element at the top level
  * Choose Item. OK
* Set action data
  * id -> @+id/action_refresh
  * Title -> Refresh (Add new string in resource)
  * Download refresh icon from [here](https://cloudup.com/cpWbpbapLbO)
  * Set refresh icon : @drawable/ic_action_refresh
  * Set show as : always
* Add handler in MainActivity

  ```
    public boolean onOptionsItemSelected(MenuItem item) {
      switch (item.getItemId()) {
        case R.id.action_refresh: {
          String token = sharedPref.getString("token", "");
          refreshNewsList(token);
          break;
        }
      }
      return true;
    } 
  ```

### Progress bar

* Add line in onCreate()

  ```
    protected void onCreate(Bundle savedInstanceState) {
      super.onCreate(savedInstanceState);
      requestWindowFeature(Window.FEATURE_INDETERMINATE_PROGRESS);
      setContentView(R.layout.activity_main);
      ...
    }
  ```
* Add in AsyncTask

  ```
    @Override
    protected void onPreExecute() {
      Log.d(TAG, "Get news started");
      setProgressBarIndeterminateVisibility(Boolean.TRUE); 
    }
  ```
* Add in AsyncTask `onPostExecute`

  ```
    setProgressBarIndeterminateVisibility(Boolean.FALSE); 
  ```

## SQLite

* Explain
  * SQLite database
  * Basic SQL command
  * Show basic command using SQLite GUI

  ```
    // create table
    CREATE TABLE news (id TEXT PRIMARY KEY, title TEXT, content TEXT)
    
    // insert into table
    INSERT INTO news VALUES('1', 'Title 1', 'Content 1')
    INSERT INTO news VALUES('2', 'Title 2', 'Content 2');
    
    // get from table
    SELECT * FROM news

    // update data in table
    UPDATE news SET content='Updated content 2' where id='2'

    // delete data from table
    DELETE FROM news WHERE id='2'
  ```

* Create NewsItem class
  * Why?
* Create SQLiteOpenHelper derived class
  * What is SQLiteOpenHelper and SQLiteDatabase

### Store news to database

* The the code after getting JSON. Where is it?

  ```
    JSONArray newsList = reader.getJSONArray("data");

    db = dbHelper.getWritableDatabase();
    
    for (int i = 0; i < newsList.length(); i++) {
      JSONObject c = newsList.getJSONObject(i);
      
      // TODO 
      // Complete the statement

      NewsItem item = new NewsItem(c.getString("_id") ... );
      dbHelper.addNews(db, item);
    }
    
    db.close();
  ```

## Show news list

### Add list view

* res/layout/activity_main.xml
* Add View
  * ListView 
* Set id for the ListView

### Add row layout

* Ctrl+N -> Android -> Android XML
* Root element : RelativeLayout
* Add View
  * ImageView
  * TextView
  * TextView
* Set id and text for each view

### Edit Main Activity

* Add function showNewsList()

```
  private void showNewsList() {
    ArrayList<NewsItem> values = dbHelper.getAllNews();

    final NewsArrayAdapter adapter = new NewsArrayAdapter(this, values);
     
    list = (ListView) findViewById(R.id.newsList);
    list.setAdapter(adapter);
  }
```

* Add new class named NewsArrayAdapter
* Task
  * What is problem with NewsArrayAdapter?

### Cursor Adapter



# News Reader phase 3

## ImageViews

* Set content in ImageView from url resource
* Use library
  * Picasso [github](http://square.github.io/picasso/)
  * Universal Image Loader for Android [github](https://github.com/nostra13/Android-Universal-Image-Loader)

* Using Picasso
  * Download jar
  * Drag and drop into libs folder in project
  * Update NewsArrayAdapter to load image using Picasso

## Sharing

## Task
  * Get news content
