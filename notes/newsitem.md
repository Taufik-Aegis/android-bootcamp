
## NewsItem class

Add new class named `NewsItem`

```
  public class NewsItem {
    
    public NewsItem(){}

    public NewsItem(String id, String title, String uri, String description, String date, String image, String content){
          this.id = id;
          this.title = title;
          this.uri = uri;
          this.description = description;
          this.date = date;
          this.image = image;
          this.content = content;
      }
      
    public String id;
    public String title;
    public String uri;
    public String description;
    public String date;
    public String image;
    public String content;
  }
```
