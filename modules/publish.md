
###### DevAcademy Android Bootcamp Notes

<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>

# App Project - Currency Converter - Publish to Google Play

## Publishing Overview

Publishing is the general process that makes your Android applications available to users. When you publish an Android application you perform two main tasks:

You prepare the application for release.
During the preparation step you build a release version of your application, which users can download and install on their Android-powered devices.
You release the application to users.
During the release step you publicize, sell, and distribute the release version of your application to users.
Usually, you release your application through an application marketplace, such as Google Play. However, you can also release applications by sending them directly to users or by letting users download them from your own website.

Figure 1 shows how the publishing process fits into the overall Android application development process. The publishing process is typically performed after you finish testing your application in a debug environment. Also, as a best practice, your application should meet all of your release criteria for functionality, performance, and stability before you begin the publishing process.

<img src="http://developer.android.com/images/publishing/publishing_overview.png" alt="Currency converter" />

Figure 1. Publishing is the last phase of the Android application development process.

## Preparing Your Application for Release

Preparing your application for release is a multi-step process that involves the following tasks:

* Configuring your application for release.

At a minimum you need to remove Log calls and remove the android:debuggable attribute from your manifest file. You should also provide values for the android:versionCode and android:versionName attributes, which are located in the <manifest> element. You may also have to configure several other settings to meet Google Play requirements or accomodate whatever method you're using to release your application.

* Building and signing a release version of your application.

The Android Development Tools (ADT) plugin and the Ant build script that are provided with the Android SDK tools provide everything you need to build and sign a release version of your application.

* Testing the release version of your application.

Before you distribute your application, you should thoroughly test the release version on at least one target handset device and one target tablet device.

* Updating application resources for release.

You need to be sure that all application resources such as multimedia files and graphics are updated and included with your application or staged on the proper production servers.

* Preparing remote servers and services that your application depends on.

If your application depends on external servers or services, you need to be sure they are secure and production ready.

You may have to perform several other tasks as part of the preparation process. For example, you will need to get a private key for signing your application, and you may need to get a Maps API release key if you are using the Google Maps external library. You will also need to create an icon for your application, and you may want to prepare an End User License Agreement (EULA) to protect your person, organization, and intellectual property.

When you are finished preparing your application for release you will have a signed .apk file that you can distribute to users.

To learn how to prepare your application for release, see Preparing for Release in the Dev Guide. This topic provides step-by-step instructions for configuring and building a release version of your application.

## Releasing Your Application to Users

You can release your Android applications several ways. Usually, you release applications through an application marketplace such as Google Play, but you can also release applications on your own website or by sending an application directly to a user.

### Releasing through an App Marketplace

If you want to distribute your apps to the broadest possible audience, releasing through an app marketplace such as Google Play is ideal.

Google Play is the premier marketplace for Android apps and is particularly useful if you want to distribute your applications to a large global audience. However, you can distribute your apps through any app marketplace you want or you can use multiple marketplaces.

### Releasing Your Applications on Google Play

Google Play is a robust publishing platform that helps you publicize, sell, and distribute your Android applications to users around the world. When you release your applications through Google Play you have access to a suite of developer tools that let you analyze your sales, identify market trends, and control who your applications are being distributed to. You also have access to several revenue-enhancing features such as in-app billing and application licensing. The rich array of tools and features, coupled with numerous end-user community features, makes Google Play the premier marketplace for selling and buying Android applications.

Releasing your application on Google Play is a simple process that involves three basic steps:

Preparing promotional materials.
To fully leverage the marketing and publicity capabilities of Google Play, you need to create promotional materials for your application, such as screenshots, videos, graphics, and promotional text.
Configuring options and uploading assets.
Google Play lets you target your application to a worldwide pool of users and devices. By configuring various Google Play settings, you can choose the countries you want to reach, the listing languages you want to use, and the price you want to charge in each country. You can also configure listing details such as the application type, category, and content rating. When you are done configuring options you can upload your promotional materials and your application as a draft (unpublished) application.
Publishing the release version of your application.
If you are satisfied that your publishing settings are correctly configured and your uploaded application is ready to be released to the public, you can simply click Publish in the developer console and within minutes your application will be live and available for download around the world.
For information complete information, see Google Play.

### Releasing your application through email

The easiest and quickest way to release your application is to send it to a user through email. To do this, you prepare your application for release and then attach it to an email and send it to a user. When the user opens your email message on their Android-powered device the Android system will recognize the APK and display an Install Now button in the email message (see figure 1). Users can install your application by touching the button.

**Notes** The Install Now button shown in Figure 1 appears only if a user has configured their device to allow installation from unknown sources and has opened your email with the native Gmail application.

Distributing applications through email is convenient if you are sending your application to only a few trusted users, but it provides few protections from piracy and unauthorized distribution; that is, anyone you send your application to can simply forward it to someone else.

### Releasing through a web site

If you do not want to release your app on a marketplace like Google Play, you can make the app available for download on your own website or server, including on a private or enterprise server. To do this, you must first prepare your application for release in the normal way. Then all you need to do is host the release-ready APK file on your website and provide a download link to users.

When users browse to the download link from their Android-powered devices, the file is downloaded and Android system automatically starts installing it on the device. However, the installation process will start automatically only if the user has configured their Settings to allow the installation of apps from unknown sources.

Although it is relatively easy to release your application on your own website, it can be inefficient. For example, if you want to monetize your application you will have to process and track all financial transactions yourself and you will not be able to use Google Play's In-app Billing service to sell in-app products. In addition, you will not be able to use the Licensing service to help prevent unauthorized installation and use of your application.

### User Opt-In for Apps from Unknown Sources

Android protects users from inadvertent download and install of apps from locations other than Google Play (which is trusted). It blocks such installs until the user opts-in Unknown sources in Settings > Security, shown in Figure 2. To allow the installation of applications from other sources, users need to enable the Unknown sources setting on their devices, and they need to make this configuration change before they download your application to their devices.

**Notes** Some network providers do not allow users to install applications from unknown sources.