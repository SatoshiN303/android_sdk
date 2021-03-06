## OAID plugin

OAID is an advertising ID that the MSA (Mobile Security Alliance) announced all Chinese-manufactured devices should provide. It is readable using the MSA SDK. You can use it to attribute and track Android devices in many markets where Google Play Services is not available. 

The OAID plugin enables the Adjust Android SDK to read a device’s OAID value *in addition* to the other device IDs it searches for by default. 

Before getting started, make sure you have read the official [Android SDK README][readme] and successfully integrated the Adjust SDK into your app.

To enable the Adjust SDK to collect and track OAID, follow these steps.

### Add the OAID plugin to your app

If you are using Maven, add the following OAID plugin dependency to your `build.gradle` file next to the existing Adjust SDK dependency:

```
implementation 'com.adjust.sdk:adjust-android:4.20.0'
implementation 'com.adjust.sdk:adjust-android-oaid:4.20.0'
```

You can also add the Adjust OAID plugin as JAR file, which you can download from our [releases page][releases].

### Add the MSA SDK to your app


To enable the OAID plugin to read OAID values using the MSA SDK, copy the MSA SDK (AAR file) to the libs directory of your project and set the dependency.  You also need to copy the supplierconfig.json to the assets directory of your project.  

You can find the MSA SDK and detailed instructions [here][msasdk].  

### Proguard settings

If you’re using Proguard and will not publish your app in the Google Play Store, you can remove all of the rules related to Google Play Services and install referrer libraries in the [SDK README][readme proguard].

Use all `com.adjust.sdk` package rules like this:

```
-keep public class com.adjust.sdk.** { *; }
```

If you are adding the MSA SDK AAR as a dependency, then add the following rules:

```
-keep class com.bun.miitmdid.core.** { *; }
```

### Use the plugin

To read OAID values, call `AdjustOaid.readOaid(applicationContext)` before starting the SDK:

```java
AdjustOaid.readOaid(applicationContext);

// ...

Adjust.onCreate(config);
```

To stop the SDK from reading OAID values, call `AdjustOaid.doNotReadOaid()`.


[readme]:    ../../../README.md
[releases]:  https://github.com/adjust/android_sdk/releases
[readme proguard]: https://github.com/adjust/android_sdk#qs-proguard
[msasdk]:  http://www.msa-alliance.cn/col.jsp?id=120
