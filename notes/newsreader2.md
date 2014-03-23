
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

### Cursor


