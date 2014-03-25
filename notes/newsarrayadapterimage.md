
## NewsArrayAdapter class with Image Loader

Add new class named `NewsArrayAdapter`

```
public class NewsArrayAdapter extends ArrayAdapter<NewsItem> {

  public NewsArrayAdapter(Context context, ArrayList<NewsItem> users) {
    super(context, R.layout.news_item, users);
  }

  @Override
  public View getView(int position, View convertView, ViewGroup parent) {
    // Get the data item for this position
    NewsItem news = getItem(position);    
    
    // Check if an existing view is being reused, otherwise inflate the view
    if (convertView == null) {
      convertView = LayoutInflater.from(getContext()).inflate(R.layout.news_item, null);
    }
    
    // Lookup view for data population
    TextView rowTitle = (TextView) convertView.findViewById(R.id.row_newsTitle);
    TextView rowDate = (TextView) convertView.findViewById(R.id.row_newsDate);
    ImageView rowImage = (ImageView) convertView.findViewById(R.id.row_newsImage);
    
    // Populate the data into the template view using the data object
    rowTitle.setText(news.title);
    rowDate.setText(news.date);

    // Set image
    Picasso.with(getContext())
      .load(news.image)
      .resize(80, 80)
      .centerCrop()
      .into(rowImage);

    
    // Return the completed view to render on screen
    return convertView;
  }
}
```