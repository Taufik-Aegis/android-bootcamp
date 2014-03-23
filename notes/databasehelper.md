
## DatabaseHelper class 

Add new class named `DatabaseHelper`

```
  public class DatabaseHelper extends SQLiteOpenHelper {

    private static final String TAG = "DatabaseHelper";

    private static final int DATABASE_VERSION = 1;
    private static final String DATABASE_NAME = "newsreader";
    private static final String TABLE_NEWS = "news";

    public static final String KEY_ID = "id";
    ...

    public DatabaseHelper(Context context) {
      super(context, DATABASE_NAME, null, DATABASE_VERSION);
    }

    @Override
    public void onCreate(SQLiteDatabase db) {
      String CREATE_NEWS_TABLE = "CREATE TABLE news ( " +
          "id TEXT PRIMARY KEY)";

      Log.d(TAG, "Create table: " + CREATE_NEWS_TABLE);
      db.execSQL(CREATE_NEWS_TABLE);
    }

    @Override
    public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {
      db.execSQL("DROP TABLE IF EXISTS " + TABLE_NEWS);
      onCreate(db);
    }

    public void addNews(SQLiteDatabase db, NewsItem item) {

      Log.d(TAG, "Add news: " + item.uri);

      ContentValues values = new ContentValues();
      values.put(KEY_ID, item.id);
      ...

      // inserting row
      db.insertOrThrow(TABLE_NEWS, null, values);
    }

    public int updateNewsContent(SQLiteDatabase db, String id, String content) {
      ContentValues values = new ContentValues();
      values.put(KEY_CONTENT, content);

      // updating row
      return db.update(TABLE_NEWS, values, KEY_ID + " = ?",
          new String[] { String.valueOf(id) });
    }

    public ArrayList<NewsItem> getAllNews() {
      ArrayList<NewsItem> newsList = new ArrayList<NewsItem>();

      String selectQuery = "SELECT  * FROM " + TABLE_NEWS;

      SQLiteDatabase db = this.getReadableDatabase();
      Cursor cursor = db.rawQuery(selectQuery, null);

      if (cursor.moveToFirst()) {
        do {
          NewsItem item = new NewsItem();
          item.id = cursor.getString(0);
          ...
          newsList.add(item);
        } while (cursor.moveToNext());
      }

      db.close();

      return newsList;
    }
  }
```