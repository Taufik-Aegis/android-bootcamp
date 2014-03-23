
# Hello world

## Create Android App

* Open Eclipse
* Run AVD
* Create new Android Project
  * File -> New -> Android Application Project
  * Fill application name
  * Modify application package name
    * typically reversed domain name + package name. Example: com.example.hello
    * must be unique. it identifies one app from another in android system
  * SDK version. use default. Next
  * Configure project. use default. Next
  * Launcher icon. use default. Next
  * Create black activity. use default. Next
  * Activity name. use default. Next
* Right click on the project
  * Run As -> Android Application
  * Choose AVD

## Explore

* AndroidManifest.xml
* src/MainActivity.java
* res/layout
* res/values
* gen/R.java
* bin/

## Android concepts

* Activity
* Layout
* Inflating layout
* Dalvik and dex
* Resource id (R.java)
* APK
* App sandbox

## ADT Tools

* Logcat 
  * Window -> Show view -> Others -> Android -> Logcat
  * Common practive : add `TAG` in class

  ```
  public class MainActivity extends Activity {

    private static final String TAG = "MainActivity";

    private void someFunction() {
      Log.v(TAG, "Just some text to log");
    }
  }
  ```

* DDMS (Dalvik Debug Monitor Server)
  * Top right of Eclipse
  * Window -> Open Perspective -> Other -> DDMS
* ADB (Android Debug bridge)
  * From Command line, type: adb, then enter
  * Useful commands
    * adb devices
    * adb kill-server
    * adb start-server
    * adb install {app.apk}
    * adb -s {device-name} shell
    * adb logcat


