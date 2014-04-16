
###### DevAcademy Android Bootcamp Notes

<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>

# App Project - Currency Converter - Phase 2

In phase 1, we have learn how to create a simple currency converter, we learn about a simple complete app, XML layout, string resource and create an event handler.

In phase 2, we will learn how to enhance previous app with multiple currencies capability. we will learn how to use `Dialog` and use `Array` to store currency data.

Adding capability to convert multiple currencies. Here, we will learn, how to use `Dialog` and use Array to store currency data.

## Add new layout

To enhance our previous apps, we don't need to create a new project, we just need to create a new xml layout and call this new layout in our `MainActivity.java` file. So instead of showing the layout `activity_main.xml` when starting our app, Currency Converter will calling our `new_xml_layout` whatever we named it.

* File -> New -> Other -> Android -> Android XML file or Use icon in toolbar or Ctrl+N -> Android -> Android XML 
* OR
* Right click on our project -> New -> Other, Select Android XML File
* Resource type is Layout. 
* Make sure we set the right project
* Fill the name (For the purpose of our example, we will named it `multiple_currency.xml`)
* Set layout to be Relative
* Next, finish.

<img src="http://imageshack.com/a/img834/4531/j5b6.jpg" alt="Add New Layout" />

## Add UI components

* Text view then edit text
* Text view then edit text
* Button
* Set id for each view

**Notes**

Set all of our UI component name in our layout using string resource like in phase 1.

<img src="http://imageshack.com/a/img838/6623/m3o1.png" alt="Set New Layout" />

## Back to Activity class

* In `onCreate` function change layout id in function `setContentView(R.layout.activity_main);` to `setContentView(R.layout.NAME_OF_NEW_LAYOUT);`
* Add onClick listener to both text view and the button
* Add `Array` to store currency data. Why Array?
* Show dialog when text view clicked. We use `AlertDialog`. 

  ```
    // list of currencies
    final CharSequence[] items = {"USD", "IDR", "SGD"};

    // initialize AlertDialog
    AlertDialog.Builder builder = new AlertDialog.Builder(this);

    // Set dialog data
    builder.setTitle("Pick a currency");

    // Handle click
    builder.setItems(items, new DialogInterface.OnClickListener() {
      public void onClick(DialogInterface dialog, int item) {
        // TODO
        // Handle item click. What behavior we expected?
      }
    });

    // create and show
    AlertDialog alert = builder.create();
    alert.show();
  ```

* Task :
  * Handle onClick in Dialog
  * We have `Array` of currencies. How we can show currency from `Array` into dialog?
  * Process conversion and show the result.

* Function to get rate from array of currencies
  ```
    private Double getCurrencyRate(String currencyStr) {
      for(int i = 0; i < rates.length; i++) {
        Currency currency = rates[i];
        if (currency.getName().equals(currencyStr)) {
          return currency.getRate();
        }
      }
      
      return 0.0;
    }
  ```
