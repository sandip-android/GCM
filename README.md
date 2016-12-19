# GCM
<H3><B>Configure Project on Firebase</B></H3>
URL : <A>https://console.firebase.google.com/</A>  
Download google-services.json file and place it into app folder
<H3><B>Declare Variables</B></H3>

public static final String SENT_TOKEN_TO_SERVER = "sentTokenToServer";  
public static final String REGISTRATION_COMPLETE = "registrationComplete";   
public static final String PREF_GCM_DEVICE_ID = "gcm_device_id";  

<H3><B>Declare Method</B></H3>
```java
public static String getGCMDeviceID(Context context) {  
	SharedPreferences sharedPreferences = PreferenceManager.getDefaultSharedPreferences(context);  
	String gcmDeviceId = sharedPreferences.getString(AppConstant.PREF_GCM_DEVICE_ID, "");  
	return gcmDeviceId;  
}
```
<H3><B>Add Permissions in Manifest.xml</B></H3>
```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="<Your Package Name>">

    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.READ_PHONE_STATE" />
    <uses-permission android:name="android.permission.GET_ACCOUNTS" />
    <uses-permission android:name="android.permission.WAKE_LOCK" />
    <uses-permission android:name="<Your Package Name>.permission.C2D_MESSAGE" />
    <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
    <uses-permission android:name="android.permission.VIBRATE" />

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">
        <activity
            android:name=".activity.MainActivity"
            android:screenOrientation="portrait">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
        
        <receiver
            android:name="com.google.android.gms.gcm.GcmReceiver"
            android:exported="true"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="gcm.play.android.samples.com.gcmquickstart" />
            </intent-filter>
        </receiver>

        <service
            android:name="com.webzino.runmile.gcm.MyGcmListenerService"
            android:exported="false">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
            </intent-filter>
        </service>
        <service
            android:name="<Your Package Name>.gcm.MyInstanceIDListenerService"
            android:exported="false">
            <intent-filter>
                <action android:name="com.google.android.gms.iid.InstanceID" />
            </intent-filter>
        </service>
        <service
            android:name="com.webzino.runmile.gcm.RegistrationIntentService"
            android:exported="false"></service>
    </application>

</manifest>
```
            
<H3><B>In build.gradle(App Level) File</B></H3>
```java
dependencies {
    compile 'com.google.android.gms:play-services:9.4.0''
}
apply plugin: 'com.google.gms.google-services'
```
<H3><B>In build.gradle(Project Level) File</B></H3>
```java
buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:2.2.3'
        classpath 'com.google.gms:google-services:3.0.0'

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}

allprojects {
    repositories {
        jcenter()
    }
}

task clean(type: Delete) {
    delete rootProject.buildDir
}
```
