
###### DevAcademy Android Bootcamp Notes

<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>

# Android SDK installation

Before we can start developing apps for Android, we need to install Android SDK (Software Development Kit) available in [Android developer website](http://developer.android.com/sdk/index.html). The Android SDK provides the API libraries and developer tools necessary to build, test, and debug apps for Android.

### Android Developer Tools (ADT Bundle)

Download ADT Bundle which include Eclipse IDE (Integrated Development Environment) and ADT plugins from [here](http://developer.android.com/sdk/index.html). ADT bundle includes :

* Eclipse + ADT plugin
* Android SDK Tools
* Android Platform-tools
* The latest Android platform
* The latest Android system image for the emulator

The choice between 32 bit and 64 bit is depend on your computer processor.

After downloading ADT, extract the zip file in your computer (for example, if using Windows to drive `C:\` then optionally rename the folder to `adt-bundle` - thus become `C:\adt-bundle`).

You should see in the `C:\adt-bundle` folder 
* eclipse/
* sdk/

#### Note on Operating System

Troughout this notes, we will use Windows as reference. However, there should be not much difference with other Operating System such as Mac OS or Linux. The difference maybe in folder name convention. For example, your ADT bundle folder might be :

* In Windows : `C:\adt-bundle`
* In Mac OS and Linux : `/FOLDER/adt-bundle`

### Installing prerequisites

Before you can run Eclipse with ADT plugins, you need to install Java JDK 6 available [here](http://www.oracle.com/technetwork/java/javase/downloads/index.html). 

Make sure Java is available on the `PATH`. To test, open `cmd.exe` then type `java -version`. If all setup correctly you will see

![Java -version](https://i.cloudup.com/_6YXO7D6qN-2000x2000.png)

#### Note on JDK and JRE

Make sure to download JDK not JRE. JDK include tools to build Java application, while JRE only include runtime to run Java application.

#### Note on JDK 7

JDK 7 is known to have compatibility issues with ADT Bundle. Make sure to install JDK version 6.

### Opening Eclipse

When all is set. Start Eclipse from `C:\adt-bundle\eclipse\eclipse.exe`. After Eclipse initialized, you will see Welcome screen. Close the Welcome screen by clicking `x` button in Android IDE tab and the Eclipse main workspace will be displayed.

