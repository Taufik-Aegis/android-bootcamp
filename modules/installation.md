
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

![Download ADT Bundle](https://i.cloudup.com/4g_jqNX328-3000x3000.png)

The choice between 32 bit and 64 bit is depend on your computer processor. However, it is easier to proceed by downloading 32 bit version for either Windows 32 bit or 64 bit.

After downloading ADT, extract the zip file in your computer (for example, if using Windows to drive `C:\` then optionally rename the folder to `adt-bundle` - thus become `C:\adt-bundle`).

You should see in the `C:\adt-bundle` folder 
* eclipse/
* sdk/

![ADT Bundle](https://i.cloudup.com/YxOdy896PL-3000x3000.png)

#### Note on ADT Bundle location

ADT Bundle location in your computer might be different from this notes. Please adjust the path accordingly when you have to deal with ADT Bundle location throughout this notes.

#### Note on Operating System

Troughout this notes, we will use Windows as reference. However, there should be not much difference with other Operating System such as Mac OS or Linux. The difference maybe in folder name convention. For example, your ADT bundle folder might be :

* In Windows : `C:\adt-bundle`
* In Mac OS and Linux : `/FOLDER/adt-bundle`

### Installing prerequisites

Before you can run Eclipse with ADT plugins, you need to install Java SE JDK 6 or 7 available [here](http://www.oracle.com/technetwork/java/javase/downloads/index.html). 

Make sure Java is available on the `PATH`. To test, open `cmd.exe` then type `java -version`. If all setup correctly you will see some lines like shown below.

![Java -version](https://i.cloudup.com/_6YXO7D6qN-2000x2000.png)

To setup Java in `PATH`, see guidelines in notes below

#### Java installation notes

* **JDK and JRE.** Make sure to download JDK not JRE. JDK include tools to build Java application, while JRE only include runtime to run Java application.
* **64 bit and 32 bit JDK.** If you choose to download 64 bit version of ADT Bundle, then you must install 64 bit version of JDK and same apply for 32 bit version. Otherwise you will see error when starting Eclipse. Note that ADT Bundle 32 bit can run in Windows 64 bit but ADT Bundle 64 bit can not run in Windows 32 bit.

##### Setup Java on Windows `Path`

These steps only applied for Windows OS. Other operating system should have their own method. Please check yourself for tutorial on internet for setup `Path` in another OS.

* Open Environment Variables dialog by right-click on Computer then click menu Properties

![Computer properties](https://i.cloudup.com/G8KQCcQ3xV-3000x3000.png)

* Click Advanced system setting then click Environment Variables.

![Environment Variables](https://i.cloudup.com/QUTpVFvAkS-3000x3000.png)

* In System Variables, Scroll down until you find `Path`, click on the `Path`, a dialog will pop up.
* In Variable value, add the following: `;C:\Program Files\Java\jdk1.7.0_51\bin`. 

![Add Java to Path](https://i.cloudup.com/KFsvOihPEE-3000x3000.png)

* *NOTE* : Make sure you set correct path pointing to Java installation. Depending on your OS, 32 or 64 bit version, the path might be `C:\Program Files (x86)\Java` or `C:\Program Files\Java`.

### Opening Eclipse

When all is set. Start Eclipse from bly clicking `eclipse.exe` in `C:\adt-bundle\eclipse\eclipse.exe`. After Eclipse initialized, you will be asked to select a workspace. You can continue with default folder shown or browse new location for workspace in your harddrive. 

![Workspace](https://i.cloudup.com/SDm3rK498f-3000x3000.png)

You will then see Contribute Usage Statistics dialog. Choose between `Yes` or `No`. You will see Android IDE Welcome screen. 

![Workspace](https://i.cloudup.com/K1RdENQiVA-3000x3000.png)

Close the Welcome screen by clicking `x` button in Android IDE tab and the Eclipse main workspace will be displayed.

![Workspace](https://i.cloudup.com/zoQ8CVPcKE-3000x3000.png)

### Troubleshooting

* Error message : `A Java Runtime Environment (JRE) or Java Development Kit (JDK) must be available ...`. This is because Java is not available in `Path`. Follow steps outlined before on how to setup Java on Windows `Path`.
* Error message : `Failed to load the JNI shared library ...`. The following can cause this error. 
  * Mismatch architecture version (32 bit/64 bit) between Eclipse in ADT Bundle and Java. If you choose to download 64 bit version of ADT Bundle, then you must install 64 bit version of JDK and same apply for 32 bit version.
  * You have more than one version of Java in your OS. Mostly you have Windows 64 bit and you have several Java installed. To force Eclipse to 
choose 64 bit version of Java, open `eclipse.ini` and add following lines  

```
  -vm
  C:\Program Files\Java\jdk\bin\javaw.exe
```
below the lines
```
  -showsplash
  com.eclipse.platform
```
so it become

```
...
  -showsplash
  com.eclipse.platform
  -vm
  C:\Program Files\Java\jdk\bin\javaw.exe
...
```

