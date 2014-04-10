
###### DevAcademy Android Bootcamp Notes

<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>

# App Project - Currency Converter - Phase 2

Adding capability to convert multiple currencies. Here, we will learn, how to use `Dialog` and use Array to store currency data.

## Add new layout

* File -> New -> Other -> Android -> Android XML file or Use icon in toolbar or Ctrl+N -> Android -> Android XML 
* Resource type is Layout. 
* Make sure we set the right project
* Fill the name
* Set layout to be Relative
* Next, finish.

## Add UI components

* Text view then edit text
* Text view then edit text
* Button
* Set id for each view

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
