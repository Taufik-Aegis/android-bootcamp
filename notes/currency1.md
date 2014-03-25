
# Currency Converter version 1

## Create Android App

* Explained in [helloworld](helloworld.md)

## Layout

* Open res/layout/activity_main.xml
* In Graphical mode, add
  * Text view
  * Edit text
  * Button
* In Outline, edit id and text each UI component
* Use string resource for text

```
For now, we will handle one USD to IDR only
```
```
use ctrl+space for eclipse autocomplete
```

## Handle click event

* Add in Button (in XML mode)
  
  ```
    android.onClick = "onClicked"
  ```

* Add onClick listener in Activity

  ```
    public void onClicked(View v) {
      ...
    }
  ```

* Add code to
  * Get view that we want to interact programmatically using `findViewById(int)`
      * `int` is resource id
      * `findViewById(int)` will return `View` object so we need to cast it to the right type. Remember Java inheritance.
  * Get input
  * Process conversion
  * Set output

  ```
    public void onClicked(View v) {
      // constant
      double USDTORP = 11400;
      // get input view
      EditText input = (EditText) findViewById(R.id.editTextInput);
      // get input value
      double inputValue = Double.parseDouble(input.getText().toString());
      // get output view
      TextView output = (TextView) findViewById(R.id.textViewOutput);
      // process conversion
      double outputValue = USDTORP * inputValue;
      // set output view value
      output.setText(((Double)outputValue).toString());
    }
  ``` 

* Try click the button with input empty
* Task
  * How to prevent that?

* Use toast to notify user
  ```
  Toast.makeText(getApplicationContext(), "Input cannot empty", Toast.LENGTH_SHORT).show();
  ```

# Currency Converter version 2

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
  * We have `HashMap` of currencies. How we can show currency from `HashMap` into dialog?
  * Process conversion and show the result.
