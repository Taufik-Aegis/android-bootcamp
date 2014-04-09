
###### DevAcademy Android Bootcamp Notes

<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>

# Android App Component

Android app components also known as main building blocks are components that you use as an application developer to build Android apps. They are the conceptual items that you put together to create abigger whole. When you start  thinking about your application, it is good to take a top-down approach. You design your application in terms of screens, features, and the interactions between them.

There are four different types of app components. Each type serves a distinct purpose and has a distinct lifecycle that defines how the component is created and destroyed. Lists of Android app components :

* Activities
* Services
* Content providers
* Broadcast receivers

In Android project, app components in one app are listed in **AndroidManifest.xml**.

We will describe each of the components above, and also discuss about **Intent** which is a messaging object you can use to request an action from another app component. 

Throughout this bootcamp, we will use Activities and Intents in our app. Services, Content providers and Broadcast receivers are provided in advanced courses.

## 1. Activity

An activity represents a single screen with a user interface where user can interact in order to do something. For example, an message app might have one activity that shows a list of your conversation and another activity to compose and send new message. Although the activities work together to form a cohesive user experience in the contact app, each one is independent of the others. As such, a different app can start any one of these activities (if the message app allows it). For example, a contact app can start the activity in the message app that composes new message, in order for the user to send a message to the specified contact. 

<img src="https://i.cloudup.com/WFQ2jZcLM4-3000x3000.png" alt="Message app" style="width: 400px;"/>

We can use a website as an analogy for activities. Just like a website consists of multiple pages, so does an Android application consist of multiple activities.

An application usually consists of multiple activities that are loosely bound to each other. Typically, one activity in an application is specified as the "main" activity, which is presented to the user when launching the application for the first time. Activities in one app declared in AndroidManifest.xml file as shown below.

```
    ...
    <application
        android:allowBackup="true"
        android:icon="@drawable/ic_launcher"
        android:label="@string/app_name"
        android:theme="@style/AppTheme" >
        <activity
            android:name="com.mygreatcompany.hello.MainActivity"
            android:label="@string/app_name" >
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>
    ...
```

We have one Activity named `com.mygreatcompany.hello.MainActivity` and since its currently our only Activity, it is also the "main" Activity, indicated by `android.intent.action.MAIN` inside the Activity tag.

### Creating an Activity

To create an activity, you must create a subclass of `Activity` (or an existing subclass of it). In your subclass, you need to implement callback methods that the system calls when the activity transitions between various states of its lifecycle, such as when the activity is being created, stopped, resumed, or destroyed. The two most important callback methods are:

* `onCreate()`. The system calls this when creating your activity. Within your implementation, you should initialize the essential components of your activity. Most importantly, this is where you must call `setContentView()` to define the layout for the activity's user interface. 

* `onPause()`. The system calls this method as the first indication that the user is leaving your activity (though it does not always mean the activity is being destroyed). This is usually where you should commit any changes that should be persisted beyond the current user session (because the user might not come back).

When you created new Android project, you will have one main Activity. You can see its implementation in **MainActivity.java**

```
public class MainActivity extends Activity {

  @Override
  protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
  }

  @Override
  public boolean onCreateOptionsMenu(Menu menu) {
    // Inflate the menu; this adds items to the action bar if it is present.
    getMenuInflater().inflate(R.menu.main, menu);
    return true;
  }
}
```

We create Activity subclass `MainActivity` which extends `Activity`. We also already implemented `onCreate()` method containing `setContentView()` method and passed `activity_main.xml` resource ID. This means, current `MainActivity` will display view as defined in `activity_main.xml`.

### Inflating XML Layout

The most common way to define a layout using views is with an XML layout file saved in your application resources. This way, you can maintain the design of your user interface separately from the source code that defines the activity's behavior. Note that you also can create layout using Java code, but we will not discuss this because it is not common approach. 

When your app get executed (when user launch the app) all the XML is actually **inflated** into Java memory space as if you actually wrote Java code. So, it’s only Java code that runs. **Inflating** is a process when XML layout resource is parsed and converted into a hierarchy of View objects in Java.

### Activity Lifecycle

Activity in Android is managed by **Activity Manager**. Activity Manager is responsible for creating, destroying, and managing activities. For example, when the user starts an application for the first time, the Activity Manager will create its activity and put it onto the screen. Later, when the user switches screens, the Activity Manager will move that previous activity to a holding place. This way, if the user wants to go back to an older activity, it can be started more quickly. Older activities that the user hasn’t used in a while will be destroyed in order to free more space for the currently active one. This mechanism is designed to help improve the speed of the user interface and thus improve the overall user experience.  

An activity can exist in essentially three states:

* **Resumed**. The activity is in the foreground of the screen and has user focus. (This state is also sometimes referred to as "running".)
* **Paused**. Another activity is visible on top of this one and that activity is partially transparent or doesn't cover the entire screen. This usually in transition stage between two activities or when dialog boxes that come up in front of an activity.
* **Stopped**. The activity is completely obscured by another activity (the activity is now in the "background"). It is no longer visible to the user and it can be killed by the system when memory is needed elsewhere.

When an activity transitions into and out of the different states described above, it is notified through various callback methods. All of the callback methods are hooks that you can override to do appropriate work when the state of your activity changes. 

<img src="http://developer.android.com/images/training/basics/basic-lifecycle.png" alt="Lifecycle" style="width: 500px;"/>

Currently we only implemented `onCreate()` callback. `onCreate()` callback is mandatory. You, as developer is recommended to implement another callback so the app respond appropriately to state changes. Below is skeleton code that implements all Activity callback.

```
public class ExampleActivity extends Activity {
    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        // The activity is being created.
    }
    @Override
    protected void onStart() {
        super.onStart();
        // The activity is about to become visible.
    }
    @Override
    protected void onResume() {
        super.onResume();
        // The activity has become visible (it is now "resumed").
    }
    @Override
    protected void onPause() {
        super.onPause();
        // Another activity is taking focus (this activity is about to be "paused").
    }
    @Override
    protected void onStop() {
        super.onStop();
        // The activity is no longer visible (it is now "stopped")
    }
    @Override
    protected void onDestroy() {
        super.onDestroy();
        // The activity is about to be destroyed.
    }
}
```

Example cases for implementing Activity callback are: 
* Write to the database during `onPause()` when the first activity stops so that the following activity can read it.
* Stop playing music when app is going to background because another app is launched.
* Save the activity state `onPause()` so we can restore it in case the app is force closed by user or destroyed by system in order to recover memory.

## 2. Services

A service is a component that runs in the background to perform long-running operations or to perform work for remote processes. A service does not provide a user interface. For example, a service might play music in the background while the user is in a different app, or it might fetch data over the network without blocking user interaction with an activity. Another component, such as an activity, can start the service and let it run or bind to it in order to interact with it.

## 3. Content providers

A content provider manages a shared set of app data. You can store the data in the file system, an SQLite database, on the web, or any other persistent storage location your app can access. Through the content provider, other apps can query or even modify the data (if the content provider allows it). For example, the Android system provides a content provider that manages the user's contact information. As such, any app with the proper permissions can query part of the content provider (to get contact data) to read and write information about a particular person.

Content providers are also useful for reading and writing data that is private to your app and not shared. 

## 4. Broadcast receivers

A broadcast receiver is a component that responds to system-wide broadcast announcements. Many broadcasts originate from the system—for example, a broadcast announcing that the screen has turned off, the battery is low, or a picture was captured. Apps can also initiate broadcasts—for example, to let other apps know that some data has been downloaded to the device and is available for them to use. 

## Intent

An Intent is a messaging object you can use to request an action from another app component. They trigger an activity to start up, tell a service to start or stop, or sending broadcasts. Intents are asynchronous, meaning the code that sends them doesn’t have to wait for them to be completed.

There are two types of intents:

* Explicit intents specify the component to start by name (the fully-qualified class name). You'll typically use an explicit intent to start a component in your own app, because you know the class name of the activity or service you want to start. For example, start a new activity in response to a user action or start a service to download a file in the background.
* Implicit intents do not name a specific component, but instead declare a general action to perform, which allows a component from another app to handle it. For example, if you want to show the user a location on a map, you can use an implicit intent to request that another capable app show a specified location on a map

