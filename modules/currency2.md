
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

To enhance our previous apps, we don't need to create a new project, we just need to create a new xml layout and call this new layout in our `MainActivity.java` file. So instead of showing the layout `activity_main` when starting our app, Currency Converter will calling our `new_xml_layout` whatever we named it.

* File -> New -> Other -> Android -> Android XML file or Use icon in toolbar or Ctrl+N -> Android -> Android XML 
* OR
* Right click on our project -> New -> Other, Select Android XML File
* Resource type is Layout. 
* Make sure we set the right project
* Fill the name (For the purpose of our example, we will named it `multiple_currency`)
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
* Add `android:clickable="true"` in both text view
* Add `Array` to store currency data. Why Array?
* Add code below in every onClick listener of text view
* Show dialog when text view clicked. We use `AlertDialog`. 

  ```
    final TextView textView = (TextView) v;
    // textView.setText("Input");

    // list of currencies
    final CharSequence[] items = { "USD", "JPY", "EUR", "SGD", "KRW",
        "GBP", "IDR" };

    // initialize AlertDialog
    AlertDialog.Builder builder = new AlertDialog.Builder(this);

    // Set dialog data
    builder.setTitle("Pick a currency");

    // Handle click
    builder.setItems(items, new DialogInterface.OnClickListener() {
      public void onClick(DialogInterface dialog, int item) {
        // TODO
        // Handle item click. What behavior we expected?
        // Ambil Item, tergantung dari item yang di klik
        textView.setText(items[item]);
      }
    });

    // create and show
    AlertDialog alert = builder.create();
    alert.show();
  ```
To store our currency data we use `Array`. First we create a new class to store our data needs. This class can hold two data, currency Name and it's rate.

Right click on our project -> New -> Class. Give this class name `Currency`.

<img src="http://imageshack.com/a/img843/2458/eztn.png" alt="Create New Class" />

Type this code in our `Currency` class.

```
public class Currency {

  private String name;
  private Double rate;
  
  //constructor
  public Currency (String _name, Double _rate)
  {
    this.name = _name;
    this.rate = _rate;
  }
  
  public String getName() {
    return name;
  }
  public void setName(String name) {
    this.name = name;
  }
  
  public Double getRate() {
    return rate;
  }
  public void setRate(Double rate) {
    this.rate = rate;
  }
}
```

Add this right after MainActivity class
```
private Currency[] rates = new Currency[7]; 
```
This code will create 7 instance of `Currency` class, where each instance will hold one currency (both name and it's rate). After we create an `Array` of `Currency` class and then we initialized it. 

Type this code in onCreate method to set it's currency name and rate.
```
    // Rates
    rates[0] = new Currency("USD", 1.00);
    rates[1] = new Currency("JPY", 102.00);
    rates[2] = new Currency("EUR", 0.72);
    rates[3] = new Currency("SGD", 1.27);
    rates[4] = new Currency("KRW", 1078.60);
    rates[5] = new Currency("GBP", 10.60);
    rates[6] = new Currency("IDR", 11395.33);
```

After we created an `Array` of `Currency` list we can use it in convert method. This method will convert value of input currency to destination currency that we choose.

```
  public void onConvertClick(View v){
    // Get input value
    EditText editText = (EditText) findViewById(R.id.inputField);
    String input = editText.getText().toString();

    if (input.equals("")) {
      Toast.makeText(getApplicationContext(),
          "Nilai tukar tidak boleh kosong", Toast.LENGTH_SHORT)
          .show();
      return;
    }

    double inputValue = Double.parseDouble(input);

    // Get currency
    TextView textView = (TextView) findViewById(R.id.inputText);
    String inputCurrency = textView.getText().toString();

    // Get output currency
    TextView textView2 = (TextView) findViewById(R.id.outputText);
    String outputCurrency = textView2.getText().toString();

    // input and output rate
    Double inputRate = getCurrencyRate(inputCurrency);

    Double outputRate = getCurrencyRate(outputCurrency);

    // konversi
    Double outputValue = inputValue / inputRate * outputRate;

    // tampilkan outputvalue-nya
    EditText editTextOutput = (EditText) findViewById(R.id.outputField);
    editTextOutput.setText(outputValue.toString());   
  }
```

To get the currency rate of input that we choose, we are using this code below.

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

This currency converter app in phase 2 will convert whatever currency we choose as input to whatever currency we choose as output. Every currenncy has it's own name and rate where it's value is hardcoded in our java code.

<img src="http://imageshack.com/a/img843/3742/hq35.jpg" alt="Currency Converter Phase 2" />
