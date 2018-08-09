---
title: "React Native Install"
date: 2018-02-10T21:44:04-08:00
draft: true
---

This post will cover React Native, and how to get started.

# What is React Native?
It is a javascript framework that allows you to write mobile applications with Javascript. The JS code you write will be converted to become native code on iOS/Android. Mobile devices create an environment that will interpret the javascript in a React style. So For example, when using a <View> component within your React-Native app, upon loading, <View> will resolve to UIView on iOS and on Android, android.view. It bridges javascript to native code... Radical!

# How do I get started?
*Note, you may use an emulator/simulator or a physical device.
*On Windows only an Android emulator is available.
*On OSX Android emulator & iOS simulators are an available option.

### Step 1
I firstly recommend installing yarn as it tends to handle the installation of dependencies better and ensures a consistent environment:  
[https://yarnpkg.com/lang/en/docs/install/](https://yarnpkg.com/lang/en/docs/install/)

### Step 2
After that install the stable version of Node (currently: 8.9.4):  
[https://nodejs.org/en/download/]
(https://nodejs.org/en/download/)

### Step 3
Node package manager is included with your Node install.
The next step is to install "create-react-native-app"
An npm package that will yield a react native app. Here is a link to the git
repository that we will be installing, with npm:  
[https://github.com/react-community/create-react-native-app]
(https://github.com/react-community/create-react-native-app)

```
$ npm install -g create-react-native-app
$ create-react-native-app my-app
$ cd my-app/
$ yarn
$ npm start
```
If you have an issue running the first command, one problem may be that you
are not running in administrative mode (sudo).

### Step 4
Once you run npm start you will see a QR code appear on your screen.
If you do...goooood you are in the matrix! BUTT, You need to create an expo account, because they require that you have an account. Visit expo.io or:   
[https://expo.io/signup](https://expo.io/signup)
And then if you open that app on your phone, you will be able to QR scan and open the app.

### Step 5 - Install Expo XDE
XDE Is Expo's Expo Dev. Environment. It is a GUI interface for scanning QR codes, running emulators, and also provides a nice interface
for debug logs.
[https://docs.expo.io/versions/latest/introduction/installation.html](https://docs.expo.io/versions/latest/introduction/installation.html)

### Step 6 - Physical Device - Optional
If you have a physical device, and want to run your app on it, download "Expo" from your respective device's store...  
Android: [https://play.google.com/store/](https://play.google.com/store/apps/details?id=host.exp.exponent&hl=en)  
iOS: [https://itunes.apple.com/us/app/expo-client/](https://itunes.apple.com/us/app/expo-client/id982107779?mt=8)

### Step 7 - iOS Simulator (Emulator) - Optional
The simulator in iOS is easy to figure out. First, download XCode and open Xcode.
Go to Preferences > Components, and download the iOS Simulator version you want.

### Step 8 - Android Emulator - Optional

##### Android Studio
I recommend installing Android Studio, as the GUI will allow you to select which versions of devices you want (easier imo).
[https://developer.android.com/studio/index.html](https://developer.android.com/studio/index.html)
If it is your first time installing Android Studio, select "Android SDK" & "Android Virtual Device". Then Open Android Studio when it is done.
If prompted when starting A.S., a "standard" setup installation will be a good option. Continue...

##### Android Studio - System Settings -> Android SDK
When the editor is open, in the upper left go to file > settings > apperance & behavior > system settings > Android sdk

On the SDK Subtab, you will see a wide variety of Android versions. I suggest  selecting 6.0 Marshmallow (Android 23). Then go to the SDK Tools subtab and select Intel x86 Emulator Accelerator (HAXM installer), Android SDK Platform-Tools, Android SDK Tools, and Android SDK Build Tools. Hit apply!
And when it is complete, select Finish. On the same settings

##### Path Variables on Windows:
Browse for your adk's tools and platform tools folder:
Mine were in **C:\Users\Me\AppData\Local\Android\sdk\platform-tools**  
**C:\Users\Me\AppData\Local\Android\sdk\tools**
You need to add those 2 paths to your User system variables.

Then under System Variables, we will be adding "ANDROID_HOME" & "ANDROID_SDK_HOME" & "JAVA_HOME"
ANDROID_HOME & ANDROID_SDK_HOME are each a variable pointing to your Android sdk path:  
**C:\Users\Me\AppData\Local\Android\sdk\**

JAVA_HOME is 1 variable pointing to your java jdk:
**C:\Program Files\Java\jdk1.8.0_144**

Last step! Create Android Virtual Device:
In the upper right of Android Studio, click AVD Manager (has the bugdroid and a purple phone as the icon.)
Select an Android device (I will be using Nexus 6p). Go to x86 images and select the system image you want (or download it), I am using Nougat. Hit next. Finish.

Then when you go to the AVD Manager, you can hit play and then your Android emulator should be running.
After than you can open EXPO XDE, ensure your emulator is running, and then on XDE click "Device" -> "Open on Android"
