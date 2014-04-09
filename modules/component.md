
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

## 1. Activity

An activity represents a single screen with a user interface where user can interact in order to do something. For example, an email app might have one activity that shows a list of new emails, another activity to compose an email, and another activity for reading emails. Although the activities work together to form a cohesive user experience in the email app, each one is independent of the others. As such, a different app can start any one of these activities (if the email app allows it). For example, a camera app can start the activity in the email app that composes new mail, in order for the user to share a picture. As such, activities are the most visible part of your application.

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

We create Activity subclass `MainActivity` which extends `Activity`. We also already implemented `onCreate()` method contains `setContentView()` method and passed `activity_main.xml` resource ID. This means, current `MainActivity` will display view as defined in `activity_main.xml`.

### XML Layout for Activity

The most common way to define a layout using views is with an XML layout file saved in your application resources. This way, you can maintain the design of your user interface separately from the source code that defines the activity's behavior. Note that you also can create layout using Java code, but we will not discuss this because it is not common approach. 

When your app get executed (when user launch the app) all the XML is actually **inflated** into Java memory space as if you actually wrote Java code. So, it’s only Java code that runs. **Inflating** is a process that convert XML layout into Java layout. 

### Activity Lifecycle

