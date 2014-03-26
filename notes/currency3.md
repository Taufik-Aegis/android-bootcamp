
# Currency Converter addon

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