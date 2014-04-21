###### DevAcademy Android Bootcamp Notes

<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>

# App Project - News Reader Phase 1

For this project we will learn few new concept. Using API on android library, using intent to fire a new action and many other things. We have learn a basic concept how to build an application for android in our previous lesson, using Currency Converter as a project. For now we will learn through more deeply into an android development world. By building News Reader app, we hope we can master a new concept: intent, listView, API and a few other things. This app is a simple version of RSS reader in android environment. Just like fetching information on our currency converter app, this app also using internet connection and sending a request of rss in one of rss feeder service. After this rss data available and then we show this data in our list view layout that we have prepared before.

We put our new function (News Reader) by creating a new layout for user interface and a new class for the actual code to handle this new function. Just like our previous app we create new menu and if user choose this menu it will triggering new layout with a list of news we grab from rss feeder service. This rss feeder website provide us with the actual data of news information on it's website.

#### RSS

RSS (Rich Site Summary); originally RDF Site Summary; often dubbed Really Simple Syndication, uses a family of standard web feed formats to publish frequently updated information: blog entries, news headlines, audio, video. An RSS document (called "feed", "web feed", or "channel") includes full or summarized text, and metadata, like publishing date and author's name.

RSS feeds enable publishers to syndicate data automatically. A standard XML file format ensures compatibility with many different machines/programs. RSS feeds also benefit users who want to receive timely updates from favourite websites or to aggregate data from many sites.

Subscribing to a website RSS removes the need for the user to manually check the web site for new content. Instead, their browser constantly monitors the site and informs the user of any updates. The browser can also be commanded to automatically download the new data for the user.

Software termed "RSS reader", "aggregator", or "feed reader", which can be web-based, desktop-based, or mobile-device-based, present RSS feed data to users. Users subscribe to feeds either by entering a feed's URI into the reader or by clicking on the browser's feed icon. The RSS reader checks the user's feeds regularly for new information and can automatically download it, if that function is enabled. The reader also provides a user interface.

**Example**

RSS files are essentially XML formatted plain text. The RSS file itself is relatively easy to read both by automated processes and by humans alike. An example file could have contents such as the following. This could be placed on any appropriate communication protocol for file retrieval, such as http or ftp, and reading software would use the information to present a neat display to the end users.

```
<?xml version="1.0" encoding="UTF-8" ?>
<rss version="2.0">
<channel>
 <title>RSS Title</title>
 <description>This is an example of an RSS feed</description>
 <link>http://www.someexamplerssdomain.com/main.html</link>
 <lastBuildDate>Mon, 06 Sep 2010 00:01:00 +0000 </lastBuildDate>
 <pubDate>Mon, 06 Sep 2009 16:20:00 +0000 </pubDate>
 <ttl>1800</ttl>
 
 <item>
  <title>Example entry</title>
  <description>Here is some text containing an interesting description.</description>
  <link>http://www.wikipedia.org/</link>
  <guid>unique string per item</guid>
  <pubDate>Mon, 06 Sep 2009 16:20:00 +0000 </pubDate>
 </item>
 
</channel>
</rss>
```

For the purpose of this project, we use this url as our data provider `http://detik.feedsportal.com/c/33613/f/656098/index.rss`.

## Layouting User Interface and Components

Next we create a new layout for news reader function. Create new XML file for layout like in our previous tutorial. This is the layout that will show up if we click News Reader menu.

<img src="http://imageshack.com/a/img843/6695/l2ep.jpg" alt="UI and Components" />

We use ListView in our News Reader app. This is a component for viewing list of item, with it's title and it's short description. It's a suitable component for viewing our rss data. Rss data provided by our website that we requested always have title and short description data. This data that we use and we showing in our app. Drag ListView into graphical layout to use a ListView. Change it's id with easier name to remember if you want to.

<img src="http://imageshack.com/a/img836/5318/85rd.png" alt="Row Layout" />

ListView is just an container for our real data. As a placeholder of our rss data we create another layout. This layout just contain one LargeText for title of our rss data and TextView for short description of our rss data.

## Add News Reader option in Menu Bar

* Open `main.xml` file located in `Converter -> res -> menu` on Package Explorer.
* Click Add to create new menu element.
* Fill the attribute for this news reader menu.

<img src="http://imageshack.com/a/img836/7859/jdk5.png" alt="Create News Reader Menu" />

<img src="http://imageshack.com/a/img834/9064/w09g.png" alt="News Reader Menu" />

News reader menu will show up if we touch menu button on our android handset. We haven't yet create handler for this menu button.

## News Activity Intent

Create new Intent for our News Reader menu.

What is Intent?

An intent is an abstract description of an operation to be performed. An Intent provides a facility for performing late runtime binding between the code in different applications. Its most significant use is in the launching of activities, where it can be thought of as the glue between activities. It is basically a passive data structure holding an abstract description of an action to be performed.

For this purpose, we use Intent to launch our `NewsActivity` class from our `MainActivity` class.

```
		// News Reader
		case R.id.action_news:
			Intent intent2 = new Intent(getApplicationContext(), NewsActivity.class);
			startActivity(intent2);
			break;
		}
```

<img src="http://imageshack.com/a/img835/2391/7pur.png" alt="News Reader Intent" />

After create new Intent, we must register `NewsActivity` in our `AndroidManifest` xml file. If we not register this activity in our `AndroidManifest` file, our activity will not run, it will give an exception error.

```
	<activity
	android:name="com.aegis.converter.NewsActivity"
	android:label="@string/rss_reader" >
	</activity>
```

<img src="http://imageshack.com/a/img843/6859/dg0o.png" alt="News Activity in AndroidManifest xml file" />

## News Activity

Next step is we create a code that grap our data from the website and show this data to user. Create a new class for our News Reader Activity, named this class `NewsActivity`.

```
public class NewsActivity extends Activity {

	ListView list = null;

	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		requestWindowFeature(Window.FEATURE_INDETERMINATE_PROGRESS);
		setContentView(R.layout.activity_news);

		list = (ListView) findViewById(R.id.listView1);
		list.setOnItemClickListener(new OnItemClickListener() {

			@Override
			public void onItemClick(AdapterView<?> parent, View view,
					int position, long id) {
				// TODO Auto-generated method stub
				RssItem item = (RssItem) list.getItemAtPosition(position);
				Log.v("Item", "onClick : " + item.getTitle());
				Intent intent = new Intent(Intent.ACTION_VIEW, Uri.parse(item.getLink()));
				startActivity(intent);
			}
		});

		String url = "http://detik.feedsportal.com/c/33613/f/656098/index.rss";
		new DownloadRssData().execute(url);

	}

	@Override
	public boolean onCreateOptionsMenu(Menu menu) {
		// Inflate the menu; this adds items to the action bar if it is present.
		getMenuInflater().inflate(R.menu.news, menu);
		return true;
	}

	public class DownloadRssData extends AsyncTask<String, Void, ArrayList<RssItem>> {

		// fungsi dengan parameter, string... data berupa array
		@Override
		protected ArrayList<RssItem> doInBackground(String... params) {
			// TODO Auto-generated method stub

			ArrayList<RssItem> rssItems = new ArrayList<RssItem>();

			try{
				URL url = new URL (params[0]);
				RssFeed feed = RssReader.read(url);
				rssItems = feed.getRssItems();
			}
			catch(Exception e){
				e.printStackTrace();
			}

			return rssItems;
		}

		protected void onPreExecute(){
			setProgressBarIndeterminateVisibility(true);
		}

		protected void onPostExecute(ArrayList<RssItem> result) {
			for(RssItem rssItem:result){
				Log.i("RSS Reader", rssItem.getTitle());
			}

			RssArrayAdapter adapter = new RssArrayAdapter(
					getBaseContext(), R.layout.row_layout, result);

			//set adapter to listview
			list.setAdapter(adapter);

		}
	}
}
``` 

## RSS Array Adapter

Create new class for RSS Array Adapter.

What is an Adapter?

An Adapter object acts as a bridge between an AdapterView and the underlying data for that view. The Adapter provides access to the data items. The Adapter is also responsible for making a View for each item in the data set.

This adapter act as a bridge that access the rss data from the internet and show that data to the view that have created.

```
public class RssArrayAdapter extends ArrayAdapter<RssItem> {

	public RssArrayAdapter(Context context, int textViewResourceId,
			List<RssItem> objects) {
		super(context, textViewResourceId, objects);
		// TODO Auto-generated constructor stub
	}
	
	@Override
	public View getView(int position, View convertView, ViewGroup parent) {
		// TODO Auto-generated method stub
		
		  // Get the data item for this position
	    RssItem news = getItem(position);    

	    // Check if an existing view is being reused, otherwise inflate the view
	    if (convertView == null) {
	      convertView = LayoutInflater.from(getContext()).inflate(R.layout.row_layout, null);
	    }

	    // Lookup view for data population
	    TextView rowTitle = (TextView) convertView.findViewById(R.id.itemTitle);
	    TextView rowDate = (TextView) convertView.findViewById(R.id.itemDescription);

	    // Populate the data into the template view using the data object
	    rowTitle.setText(news.getTitle());
	    rowDate.setText(news.getPubDate().toString());

	    // Return the completed view to render on screen
	    return convertView;
	 
	}
}
```

<img src="http://imageshack.com/a/img845/6603/y5jl.png" alt="News Reader" />