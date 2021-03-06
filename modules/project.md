
###### DevAcademy Android Bootcamp Notes

<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>

# Android Project

Now that you know where is your app is located inside Android platform, we will take a look into our Android app project. You will learn some of the important files that make one Android app. 

## Android Project Structure

If you look into **Package Explorer** view, you will see several items with folder-like icon. ADT organized Andriod project into several folders each with different purpose.

* **src/**. This folder contains the java code. If you want to add new code or adding existing code (from your other project or other open source code) to your project, you can drag and drop the Java code here, or copy to your src project folder in Windows Explorer.
* **gen/**. This contains files generated by Android SDK. Specifically here we see **R.java**. **R.java** contains all resource files IDs (in **res** folder) so we can use it from our Java code.
* **assets/**. You can use this folder to store raw asset files. Files that you save here are compiled into an .apk file as-is, and the original filename is preserved. You don't need IDs to use files in this folder
* **bin/**. Output directory of the build. This is where you can find the final .apk file and other compiled resources. You can see file with extension .dex here. That is Dalvik VM executable file.
* **libs/**. This contains third party Java library (.jar) files that you use. You can drag and drop the .jar file here, or copy to your project libs folder in Windows Explorer.
* **res/**. Contains application resources, such as drawable files, layout files, and string values. Files that added here can be accessed from Java code using generated IDs. When your application is compiled, **aapt** (Android Asset Packaging Tool) generates the R class (located in **gen/** folder), which contains resource IDs for all the resources in your **res/** directory. You can read more about Android resource [here](http://developer.android.com/guide/topics/resources/overview.html)
  * drawable-* - Contain graphical resources (jpegs, pngs, etc) for devices with the specific resolution.  
  * layout - Layout contains xml descriptors of views. 
  * menu - The menu folder contains xml descriptors of menus. 
  * values - This folder contains xml files with key value pairs.

<img src="https://i.cloudup.com/YLTHR9rQI3-3000x3000.png" alt="Android project structure" style="width: 300px;"/>

## Android Project Files

In Android project image above, you see several files available in your project. We will take a look into some of the files to gain more understanding about Android project.

### Android Manifest

Every application must have an **AndroidManifest.xml** file (with precisely that name) in its root directory. The manifest file presents essential information about your app to the Android system, information the system must have before it can run any of the app's code. It contains information about the Android application such as app package name, minimum Android version, permission to access Android device capabilities such as internet access permission and others. It describes the components of the application — the activities, services, broadcast receivers, and content providers that the application is composed of. We will discuss Android application components later. 

This is what we have in **AndroidManifest.xml**. 

```
  <?xml version="1.0" encoding="utf-8"?>
  <manifest xmlns:android="http://schemas.android.com/apk/res/android"
      package="com.mygreatcompany.hello"
      android:versionCode="1"
      android:versionName="1.0" >

      <uses-sdk
          android:minSdkVersion="8"
          android:targetSdkVersion="18" />

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
  </manifest>
```

`@` sign (for example `@drawable/ic_launcher` and `@string/app_name`) in XML file is reference to other resource data in another file. For example, `@string/app_name` will point to data in `string` resource with name `app_name`. We will see this `string` resource later. `@drawable` will point to image located in drawables folders.

#### Note on Android Resource

**1. XML Format**
<br/>

Most of the Android resource files (with exception of images) are represented in XML format. XML stands for eXtensible Markup Language, it is one most common text file format used. It is easy to read by both human and machine. You can read more about XML [here](http://www2.informatik.hu-berlin.de/~xing/Lib/Docs/jaxp/docs/tutorial/overview/1_xml.html). Basically, XML file has tag (identifiers enclosed in angle brackets, like this: <...>) and attribute (additional information included as part of the tag itself, within the tag's angle brackets.). Simple example shown below:

```
<tag attribute="some value">This is the content of tag</tag>
```

There is no rule on how the data arranged in tag or attribute. It depends on who created the schema (XML data structure)

**2. Viewing Resource in XML**
<br/>

When you open AndroidManifest.xml, you will not see XML file directly. Eclipse will show Graphical or wizard like view which represent the XML contents so its easy to edit. If you want to see the XML content, you can switch the view, by clicking AndroidManifest.XML tab at the bottom. This also applied to any other XML files in the project. Here, I will show you only the XML code as shown previously.

<img src="https://i.cloudup.com/YrbdwcGktk-3000x3000.png" alt="Android project structure" style="width: 500px;"/>

### Layout XML File

Layout XML file is located in **res/layout/** folder. The layout file specifies the layout of your screen. Layout consists of views that create your app screen. In this case, we have only one screen (named `activity_main.xml`) and it’s loaded by the MainActivity.java. 

```
  <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
      xmlns:tools="http://schemas.android.com/tools"
      android:layout_width="match_parent"
      android:layout_height="match_parent"
      android:paddingBottom="@dimen/activity_vertical_margin"
      android:paddingLeft="@dimen/activity_horizontal_margin"
      android:paddingRight="@dimen/activity_horizontal_margin"
      android:paddingTop="@dimen/activity_vertical_margin"
      tools:context=".MainActivity" >

      <TextView
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:text="@string/hello_world" />

  </RelativeLayout>
```

In this layout file, we have on view which is `TextView` which contain attribute `android:text` point to other resource `@string/hello_world`. 

### String

String resource located in **res/values/strings.xml** . If you look to the XML content you will see something like below:

```
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string name="app_name">Hello</string>
    <string name="action_settings">Settings</string>
    <string name="hello_world">Hello world!</string>
</resources>
```

If you recall previously, in AndroidManifest.xml, we see `@string/app_name` and in `activity_main.xml` we see `@string/hello_world`. Those will point to value in this `strings` resources. If you change `<string name="hello_world">Hello world!</string>` into `<string name="hello_world">Halo, this is my great app</string>` and you re-run your app, you will see the text in app is changed.

This is the best practice for separating the concerns of various files, even if they are XML files. In other words, layout XML is responsible for the layout of widgets, but strings XML is responsible for their textual content

### R.java

When developing Android application, most of the time we will spend in resource **res/** folder and Java **src/** folder. It is important to understand relation between files and other data in **res/** to **R.java** to your Java file. The process is illustrated below.

<img src="https://i.cloudup.com/-p-NhOtoPY-3000x3000.png" alt="Resource process" style="width: 500px;"/>

1. When you compile your app, Android SDK (aapt) will generate resource ID to **R.java** file. The hexadecimal number you see (for example: 0x7f030000) is pointer to location of resource file in compiled Android resource.
1. When you want to use the resource, you access the resource using ID from **R.java**. 

We can say that **R.java** file is the glue between the world of Java and the world of resources. It is an automatically generated file, and as such, you never modify it. It is recreated every time you change anything in the res directory, for example, when you add an image or add/edit XML file.

#### Error in Accessing Resource ID 

Because Android SDK generate **R.java** file during compilation, when you have errors in your code, compilation will failed and new **R.java** will not be generated. In this case, you have to :

* Fix the error, or comment the part which cause errors in your Java code.
* In Eclipse menu, click **Project** then click **Clean...**. Then click **OK** to clean your project

<img src="https://i.cloudup.com/cHUZLT1RvZ-3000x3000.png" alt="Clean" style="width: 500px;"/>

If you notice in menu above, you see **Build Automatically** is checked. When you clean the project, Eclipse will automatically re-compile the project and **R.java** file. Eclipse also will automatically re-compile the project when you add new resource or add/edit then save Java file.

#### Resource Naming

Because resource will be compiled into R.java, its is required that resource name follow standard Java variable naming guidelines. For example, first letter should be alphabet and not numeric, and using dash (-) is not allowed. In resource, common name is using lower case separated by underscore (_). For example `app_name`.

### Java Source Code

The Java code is what drives everything. This is the code that ultimately gets converted to a Dalvik executable and runs your application. When you created an Android project, we will have one Java file named `MainActivity.java`. 

```
package com.mygreatcompany.hello;

import android.os.Bundle;
import android.app.Activity;
import android.view.Menu;
import android.widget.Button;

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

Java source code contains several parts

#### 1. Package Name

```
package com.mygreatcompany.hello;
```

This is package name that you set when you created the project. Packages are used in Java in order to prevent naming conflicts, to control access, to make searching/locating and usage of classes, interfaces and other components easier. A Package can be defined as a grouping of related types (classes, interfaces, and others) providing access protection and name space management.

#### 2. Import Packages

```
import android.os.Bundle;
...
```

You use other packages by importing their package name in your Java file using `import` keyword. 

#### 3. Java Code

This is your Java code and you will spend lots of time adding variables and methods that make your app functional. 

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

  // Your code will be here
}
```

## Application Package (APK)

In android, an app is distributed as file APK (Application Package) with extension **.apk**. APK files are a type of archive file specifically in zip format. You can use any software that can process zip file to see APK file content.

<img src="https://i.cloudup.com/zgmPCO-bSk-3000x3000.png" alt="Clean" style="width: 500px;"/>

An APK file is an archive that usually contains the following files/directories:

* **Dalvik executable**. This is all your Java source code compiled down to a Dalvik executable. This is the
code that runs your application.
* **Resources**. Resources are everything that is not code. Your application may contain a number of images and audio/video clips, as well as numerous XML files describing layouts, language packs, and so on. 
* **Native libraries**. Optionally, your application may include some native code, such as C/C++ li- braries. These libraries could be packaged together with your APK file.
* **AndroidManifest.xml**. You app manifest file
* **META-INF**. Which contain certificate of the application.

## Android Project Location in Windows Explorer

You have created new Android project in Eclipse, but where is the project files in your Windows Explorer? If you recall when you run Eclipse the first time, you are asked to set workspace folder. By default, when you create new Android project, project files will be created in the workspace folder. You can check location of your project in project properties. 

* in Eclipse menu, right-click on your project root in **Package Explorer** then click **Properties**.

<img src="https://i.cloudup.com/3d46f0_yTr-1200x1200.png" alt="Clean" style="width: 500px;"/>

* You will see project location in project property page

<img src="https://i.cloudup.com/ZmonhjR1V7-1200x1200.png" alt="Clean" style="width: 500px;"/>
