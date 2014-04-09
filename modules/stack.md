
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
