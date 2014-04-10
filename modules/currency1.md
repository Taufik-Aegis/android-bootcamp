
###### DevAcademy Android Bootcamp Notes

<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>

# App Project - Currency Converter - Phase 1

You have learn about Android architecture, app components and has created and run HelloWorld app. From now on, you will learn how to create a simple complete app, named Currency Converter. This app, will convert one currency to another. We will divide app progress into 3 phases :

* Phase 1. Simple currency converter, only handle USD to IDR. Here, we will learn, how to create XML layout and use layout item in Java code.
* Phase 2. Adding capability to convert multiple currencies. Here, we will learn, how to use `Dialog` and use Array to store currency data.
* Phase 3. Adding capability to update currency rate from internet using `HttpURLConnection`, create new thread using `AsyncTask`, process JSON data, store currency data in `SharedPreferences`, and how to use permission.

<img src="https://i.cloudup.com/Vsr6JUXboZ-3000x3000.png" alt="Currency converter" style="width: 600px;"/>

Before we create new Android project. To prevent confusion because there are files from other project opened in **Code View**, close all open files by clicking `x` (Close) in each file tab.

## Create New Project

You already know how to create Android app project in **Hello World**. Now, create new Android Application project :

* Set the app name to : Converter
* Set package name with guide as we discussed in **Hello World**
* Leave everything default, then finish.

You will see two files opened in **Code View** tabs : MainActivity.java and activity_main.xml, Now click on activity_main.xml to open it. If you don't see activity_main.xml in tab, you can open it from **Project Explorer** view by clicking `res/` the `layout/`. You can refer to notes on **Android Project** about Android project structure. 

## View and View Layout

All user interface elements in an Android app are built using `View` and `ViewGroup` objects. A `View` is an object that draws something on the screen that the user can interact with. A `ViewGroup` is an object that holds other `View` (and `ViewGroup`) objects in order to define the layout of the interface.

Android provides a collection of both `View` and `ViewGroup` subclasses that offer you common input controls (such as buttons and text fields) and various layout models (such as a linear or relative layout).

The user interface for each component of your app is defined using a hierarchy of `View` and `ViewGroup` objects. Each view group is an invisible container that organizes child views, while the child views may be input controls or other widgets that draw some part of the UI. This hierarchy tree can be as simple or complex as you need it to be (but simplicity is best for performance).

From now on, we will refer each of the UI component: button, text view and others as `View`.

<img src="https://developer.android.com/images/viewgroup.png" alt="View hierarchy" style="width: 400px;"/>

### Declarative and Programmatic Approach in Creating UI

In Android app development, when creating the UI, you start with XML file. This appoach is called Declarative approach. The declarative approach involves using XML to declare what the UI will look like, similar to creating a web page using HTML. You write tags and specify elements to appear on your screen. If you have ever handcoded an HTML page, you did pretty much the same work as creating an Android screen.

Graphical mode in Eclipse provide what-you-see-is-what-you-get (WYSIWYG) view so you can arrange your UI layout easily. However, Declarative approach do not provide ways to manipulate or handling UI event. For that purpose, we use Programmatic approach which involves referring to XML resources using its resource ID and write Java code to respond to UI event such as click and others.

### Common Layout

A layout defines the visual structure for a user interface, such as the UI for an activity or app widget. Common layout in Android SDK:

* Linear Layout. A layout that organizes its children into a single horizontal or vertical row. 
* Relative Layout. This is the default layout when you created Android project. Relative Layout enables you to specify the location of child objects relative to each other (child A to the left of child B) or to the parent (aligned to the top of the parent).
* Frame Layout. FrameLayout places its children on top of each other so that the latest child is covering the previous, like a deck of cards. This layout policy is useful for tabs, for example. FrameLayout is also used as a placeholder for other widgets that will be added programmatically at some later point in time.

## Editing Layout XML File

In Eclipse, you can edit layout file using Graphical mode or edit XML file directly. For convenience, we will using Graphical editor then edit XML file when necessary.

<img src="https://i.cloudup.com/u8JH4Trv0x-3000x3000.png" alt="Editing XML" style="width: 600px;"/>

Some of Eclipse Graphical editor that you need to know :

1. View Categories. In Graphical mode, `View` is categorized into several groups. Form Widgets contains static View which user cannot edit, but can interact with it (like tap or click). You can see in this catogory: `TextView`, `Button`, `CheckBox`, `ProgressBar` and many others.
1. Text Fields category. This category contains editable text fields such as `EditText` with several variations. There are other categories that you can explore: Layout, Composite, Images & Media and many others.
1. Scale control. You can use this to zoom-in or zoom-out the Graphical view. There are other buttons in this upper area that you can explore.
1. Outline View. Shows hierarchy representation of layout element. You can see we have `RelativeLayout` with one child `TextView`. When you add another `View` object to the layout, you will see your `View` added here.
1. Properties View. Shows property of a `View` object. For example, if you select `TextView` in the Outline View, you will see in Properties that you can change its `Id`, `Text`, `Hint` and many others. As we have mentioned before, you can edit the properties directly in XML file. 
1. Graphical and XML mode switch. You can switch between Graphical mode and XML with these buttons.

<br/>
Let's start to work.

### Add Views to Layout

Now, we will add some `Views` to our layout

1. Delete Hello World `TextView` by clicking on it and press delete.
1. Add Large `TextView` by clicking on `Large` from Form Widgets category and drag it into the layout. Since by default we have Relative Layout, you can drag the `View` until it aligned to the center.
1. Add plain text `EditText` view from Text Fields category.
1. Add another Large `TextView`
1. Add `Button`

You will have view like shown in the next image.

<img src="https://i.cloudup.com/0BIp9fVKZ4-3000x3000.png" alt="Simple currency layout" style="width: 400px;"/>

### Edit View Id

Next, we edit each of the `View` id. We want to name our `View` with easy to remember `id` names, so we can refer to it easily from our Java code. If you click one of the `View` in Outline, you can change its `id` by clicking button in `id` property. It is a good practice to change the `id` value instead of using default ones. You can also change `View` id directly in XML file.

<img src="https://i.cloudup.com/tRY4HUJPCa-3000x3000.png" alt="Simple currency layout" style="width: 500px;"/>

1. Change `textView1` to `titleText`
1. Change `editText1` to `inputCurrency`
1. Change `textView2` to `outputCurrency`
1. Change `button1` to `convertButton`

**Important**

If you don't change the `id` you might get error later when following this bootcamp notes. In example codes, we will use `id` that we use here.

### Update Text String

Android recommended us to use string resource instead of hardcode the string into `View` property directly. This will make it easier for us to support multiple language by using different string resource file. We will change text in `titleText`.

<img src="http://imageshack.com/a/img811/402/sdx3.jpg" alt="Update String Resource" />

1. On package explorer, Double click `string.xml` file located in `Converter->res->values` path and `Resources Elements` panel will show up.

2. Click `Add` Button. Dialog will show up.

3. Choose `String`, click `OK`.

4. On the right side of Resources Elements panel, type the name and value of the string resource. `Name` is the id of our string element and `Value` is the name of the string we would want to.

5. Set all of the string resource in our layout we want to change (`titleText`, `convertButton`).

**Important**

The name in input field must match with the name of if string resource, if your name and id doesn't match you might your string element will not get updated.

### Set Click Event in Layout

We want to make our apps convert currency from dollar to rupiah, so we attach event click on convert `button`.

Open `activity_main.xml` file located in `Converter->res->layout`. Select `activity_main.xml` tab, located beside Graphical Layout tab. Add `android.onClick = "onClicked"` in button xml.

### Create Event Handler

Open `MainActivity.java' file. Type code below inside MainActivity class.

```
  public void onClicked(View v) {
    // constant
    double USDTORP = 11400;

    // get input view
    EditText input = (EditText) findViewById(R.id.inputCurrency);

    // get input value
    double inputValue = Double.parseDouble(input.getText().toString());

    // get output view
    TextView output = (TextView) findViewById(R.id.outputCurrency);

    // process conversion
    double outputValue = USDTORP * inputValue;

    // set output view value
    output.setText(((Double)outputValue).toString());
  }
```

