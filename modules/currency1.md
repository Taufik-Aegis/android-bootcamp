
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

<img src="https://developer.android.com/images/viewgroup.png" alt="View hierarchy" style="width: 400px;"/>

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

### Add Views to Layout

Now, we will add some `Views` to our layout

1. Delete Hello World `TextView` by clicking on it and press delete.
1. Add Large `TextView` by clicking on `Large` from Form Widgets category and drag it into the layout. Since by default we have Relative Layout, you can drag the `View` until it aligned to the center.
1. Add plain text `EditText` view from Text Fields category.
1. Add another Large `TextView`
1. Add `Button`

You will have view like shown in the next image.

<img src="https://i.cloudup.com/0BIp9fVKZ4-3000x3000.png" alt="Simple currency layout" style="width: 400px;"/>



