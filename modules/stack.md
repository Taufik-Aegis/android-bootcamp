
###### DevAcademy Android Bootcamp Notes

<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>

# Android Stack

We have created Android app project and runs it to the emulator. Before we start working on our app, first, we will explore Android stack, Android project structure and some of Android concepts that we will use during this bootcamp. 

## Android Architecture

The Android operating system is like a cake consisting of various layers. Each layer has its own characteristics and purpose. 

<img src="https://i.cloudup.com/rGuI7rUgI_-1200x1200.jpeg" alt="Architecture" style="width: 500px;"/>

### 1. Linux 

Android is built on top of Linux. Linux is a great open source operating system. There are many good reasons for choosing Linux as the base of the Android stack. Linux is a mature project with lots of hardware abstraction related components are readily available. Linux is also a highly secure system, and all Android applications run as separate Linux processes with permissions set by the Linux system. 

#### Sandboxing

Running each application as separate processes with different permissions is known as Sandboxing. Sandbox isolates your app data and code execution from other apps. One application cannot access data in another application sandbox without explicit permission. 

### 2. Native Libraries and Android Runtime

#### Native Libraries

The native libraries are C/C++ libraries, often taken from the open source community in order to provide necessary services to the Android application layer. Some of the libraries are: 

* **Webkit** A fast web-rendering engine used by Safari, Chrome, and other browsers
* **SQLite** A full-featured SQL database
* **OpenGL** 3D graphics libraries
* **OpenSSL** The secure locket layer
* And many others.

#### Android Dalvik Virtual Machine

Android use Java as primary programming language. Java compiles into bytecode and then executed on Java Virtual Machine (VM). By using Java VM, it is possible to execute Java code on every machine that runs Java VM without have to recompile the Java code. 

For Android, team at Google created new virtual machine named **Dalvik** designed specifically for mobile devices which has constraint on battery life and processing power. This makes compilation process a bit different from standard Java. After you created Java bytecode, you recompile it once again using the Dalvik compiler to Dalvik byte code. It is this Dalvik byte code that is then executed on the Dalvik VM.

<img src="https://i.cloudup.com/EEv3WcmWgo-3000x3000.png" alt="Dalvik VM" style="width: 400px;"/>

Dalvik is based on JIT (just in time) compilation. It means that each time you run an app, the part of the code required for its execution is going to be translated (compiled) to machine code at that moment. As you progress through the app, additional code is going to be compiled and cached, so that the system can reuse the code while the app is running. Since JIT compiles only a part of the code, it has a smaller memory footprint and uses less physical space on the device. However, there will be lag from the moment you click the app until its running.

#### New Android Runtime

As a part of Android 4.4 KitKat, Google introduced a new way of executing apps on top of the Android OS. Then new runtime, named **ART (Android Runtime)**, compiles the Dalvik bytecode, into a system-dependent binary. The whole code of the app will be pre-compiled during install, called AOT (Ahead of Time) compilation. ART will generally make app execute mush faster. ART, however, increase the binary size of the app and takes a bit longer to install because of compilation process.

Currently ART status is still ongoing project and experimental. In KitKat, You can choose to use ART by going to **Settings > Developer Options > Select Runtime** and choosing ART.

<img src="https://i.cloudup.com/NISlw1PONj-3000x3000.png" alt="ART" style="width: 250px;"/>

### 3. Application Frameworks

The application framewoks consists of numerous Java libraries specifically built for Android. This is the most important and the most extensively covered part of the Android platform because this is the layer that provide capabilities for app development such as location, WiFi, contacts, notification, messaging, telephony and so on. 

During this bootcamp, you will learn several Android frameworks used in Android app development. For more documentation on all of Android frameworks, you can check [Android developer website](http://developer.android.com/guide/index.html)

### 4. Applications

At the top layer of Android stack is Applications or **apps**. these are the apps that you and other developers create. These apps are what end users find valuable about Android. They can come preinstalled on the device or can be downloaded from one of the many Android markets.

## Android Project Structure

Now that you know where is your app is located inside Android platform, we will take a look into our Android app project. You will learn some of the components that make one Android app. 

<img src="https://i.cloudup.com/YLTHR9rQI3-3000x3000.png" alt="Android project structure" style="width: 300px;"/>

If you look into **Package Explorer** view above, you will see several items with folder-like icon. ADT organized Andriod project into several folders each with different purpose.

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

When you open AndroidManifest.xml, you will not see XML file directly. Eclipse will show view which represent the XML contents so its easy to edit. If you want to see the XML content, you can switch the view, by clicking AndroidManifest.XML tab at the bottom. This also applied to any other XML files in the project. Here, I will show you only the XML code as shown previously.

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

