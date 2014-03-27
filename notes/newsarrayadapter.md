
## NewsArrayAdapter class

Add new class named `NewsArrayAdapter`

```
public class NewsArrayAdapter extends ArrayAdapter<RssItem> {

  public NewsArrayAdapter(Context context, ArrayList<RssItem> users) {
    super(context, R.layout.news_item, users);
  }

  @Override
  public View getView(int position, View convertView, ViewGroup parent) {
    // Get the data item for this position
    RssItem news = getItem(position);    
    
    // Check if an existing view is being reused, otherwise inflate the view
    if (convertView == null) {
      convertView = LayoutInflater.from(getContext()).inflate(R.layout.news_item, null);
    }
    
    // Lookup view for data population
    TextView rowTitle = (TextView) convertView.findViewById(R.id.itemTitle);
    TextView rowDate = (TextView) convertView.findViewById(R.id.itemDate);
    
    // Populate the data into the template view using the data object
    rowTitle.setText(news.title);
    rowDate.setText(news.date);
    // TODO, set image
    
    // Return the completed view to render on screen
    return convertView;
  }
}
```