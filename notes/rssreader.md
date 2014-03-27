
# RSS Reader

## Add RSS Reader library

* Download library from [here](https://github.com/matshofman/Android-RSS-Reader-Library)
* Extract and copy to src folder of the project

## Add AsyncTask to download RSS using background thread

  ```
    private class DownloadRSSData extends AsyncTask<String, Void, ArrayList<RssItem>> {

      @Override
      protected ArrayList<RssItem> doInBackground(String... params) {
        // TODO Auto-generated method stub
        return null;
      }
      
      protected void onPostExecute(ArrayList<RssItem> result) {
        
      }
    }
  ```

## Add download RSS code in `doInBackground`

  ```
    ArrayList<RssItem> rssItems = new ArrayList<RssItem>();
    
    try {
      URL url = new URL(params[0]);
      RssFeed feed = RssReader.read(url);
      rssItems = feed.getRssItems();
    }
    catch (Exception e) {
      e.printStackTrace();
    }
    
    return rssItems;
  ```

* Task
  * Why we add try catch block?
  * How the code changes when we add try-catch

## Show result in log
  ```
    protected void onPostExecute(ArrayList<RssItem> result) {
      for(RssItem rssItem : result) {
          Log.i("RSS Reader", rssItem.getTitle());
      }
    }
  ```

## Execute task
  ```
    
  ```
