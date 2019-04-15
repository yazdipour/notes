# Android

## DB

* Realm: https://virgool.io/@sjd.noroozi91/بلعیدن-شیرینی-دانمارکی-یا-راهکاری-برای-قورت-دادن-استوانه-ها-mcftjpolptjs
* KeyValue: SnappyDB
* ORM: ActiveAndroid, SugarORM, DBFlow

## Amazing open source Android apps

* https://github.com/Mybridge/amazing-android-apps/blob/master/README.md

## IntentFilter


```xml
<activity android:name=".HelloWorld"
    android:label="@string/app_name">
    <intent-filter>
        <action android:name="android.intent.action.VIEW"/>
        <category android:name="android.intent.category.DEFAULT"/>
        <category android:name="android.intent.category.BROWSABLE"/>
        <data android:scheme="http" android:host="androidium.org"/>
    </intent-filter>
</activity>
```

To test:
`startActivity(new Intent (Intent.ACTION_VIEW, Uri.parse("http://androidium.org")));`

## Simple RX

```java
        boolean ready = false;
        Observable<Boolean> observable = Observable.just(ready);
        Observer<Boolean> observer = new Observer<Boolean>() {
            @Override
            public void onSubscribe(Disposable d) {
            }

            @Override
            public void onNext(Boolean aBoolean) {
                // DO SOMETHING
            }

            @Override
            public void onError(Throwable e) {
            }

            @Override
            public void onComplete() {
            }
        };
        observable.subscribe(observer);
```

## Caching Retrofit

https://medium.com/mindorks/caching-with-retrofit-store-responses-offline-71439ed32fda

## Get Package Version

```java
try {
    PackageInfo pInfo = context.getPackageManager().getPackageInfo(getPackageName(), 0);
    String version = pInfo.versionName;
    int verCode = pInfo.versionCode;
} catch (PackageManager.NameNotFoundException e) {
    e.printStackTrace();
}
```

## SocketIO

https://socket.io/blog/native-socket-io-and-android

```java
mSocket = IO.socket("http://chat.socket.io");
mSocket.connect();
mSocket.emit("new message", message); //Emitting events - Sending data
mSocket.on("new message", onNewMessage); //Listening on events
mSocket.off("new message", onNewMessage);
private Emitter.Listener onNewMessage = new Emitter.Listener() {
    @Override
    public void call(final Object.. args) {
        getActivity().runOnUiThread(new Runnable() {
            @Override
            public void run() {
                JSONObject data = (JSONObject) args[0];
```

## Binding

add in app/build.gradle

```gradle
android {
    // Previously there
    // Add this next line
    dataBinding.enabled = true
```

```java
class model implement BaseObservable{
    //2way
    @Bindable
    public int setP(int x){
        p=x;
        notifyPropertyChanged(BR.p);
    }
    public int getP(){}
}

class model2 implement Observable{
    private PropertyChangeRegistry pcr;
    //2way
    @Bindable
    public int setP(int x){
        p=x;
        pcr.notifyPropertyChanged(BR.p);
    }
    public int getP(){}
}

class Activty{
    ActivityMainBinding binding = DataBindingUtil.setContentView(this, R.layout.activity_main);
    binding.setP(user)
}
```

```xml
<layout xmlns:android="http://..."
        xmlns:tools="http://...">
    <data>
        <import type="android.view.View" />

        <variable name="user" type="com.example.User"/>
    </data>

    <TextView
    android:visibility="@{bool1? View.VISIBLE:View.GONE}"
    android:text="@{@string/pFormat{p.Name}}"
    android:text2="@={p.Age, default=my_default}"
    app:onRefreshListener="@{() -> yourViewFragment.refreshList()}"
    />
```


# Resources

- https://androidresources.net/
- [Libraries](https://android-arsenal.com/)
- [Libraries⭐](https://fossdroid.com)
- [Svg2Drawable](http://inloop.github.io/svg2android/)
- [OneSignal](https://onesignal.com/apps/8e8fc011-b4da-4d3f-88ec-f170bcddd292)
- [Farsi Tutorial](https://programchi.ir/)
- [Tutorial Futurestud](https://futurestud.io/)
- https://material.io/icons/#ic_done
- https://romannurik.github.io/AndroidAssetStudio/index.html

## Iranian Store

- https://developer.myket.ir/applications?type=grid
- https://cafebazaar.ir/developers/panel/apps/?l=fa
- http://developer.iranapps.ir/user/login
- http://www.plazza.ir/repoz
- http://cando.asr24.com/user/
- http://dgad.ir/panel/apps/

### Kotlin

- https://kotlin.link/?q=%20
- https://hackr.io/tutorials/learn-kotlin

### Animations

- [Rebound](https://github.com/facebook/rebound) - Rebound is a Java library that models spring dynamics.
- [Android View Animations](https://github.com/daimajia/AndroidViewAnimations) - Cute view animation collection.
- [Android-Transition](https://github.com/kaichunlin/android-transition) - Allows the easy creation of view transitions that react to user inputs.
- [Android-View-Actions](https://github.com/dtx12/AndroidAnimationsActions) - Makes creating complex animations for views easy.
- [Swipper](https://github.com/mdg-iitr/Swipper) - Android library for swipeable gestures to control volume , brightness and seek .
- [Spotlight](https://github.com/TakuSemba/Spotlight) - Android Library that lights items for tutorials or walk-throughs etc...

### Security

- [libsignal-protocol-java](https://github.com/signalapp/libsignal-protocol-java) - A ratcheting forward secrecy protocol that works in synchronous and asynchronous messaging environments.
- [Themis](https://github.com/cossacklabs/themis) - Multi-language framework for making typical encryption schemes easy to use: data at rest, authenticated data exchange, transport protection, authentication, and so on.

### Date & Time

- [ThreeTen Android Backport](https://github.com/JakeWharton/ThreeTenABP) - An adaptation of the JSR-310 backport for Android.
- [Joda-Time Android](https://github.com/dlew/joda-time-android) - Joda-Time library with Android specialization.
- [True Time](https://github.com/instacart/truetime-android) - Android NTP time library. Get the true current time impervious to device clock time changes.

### Runtime Permissions

- [Permission Dispatcher](https://github.com/permissions-dispatcher/PermissionsDispatcher) - Simple annotation-based API to handle runtime permissions.
- [RxPermissions](https://github.com/tbruyelle/RxPermissions) - Android runtime permissions powered by RxJava.
- [NoPermission](https://github.com/NoNews/NoPermission) - Simple Android library for permissions request. Consists of only one class.

### Debugging Tools

- [Linx](https://github.com/pedrovgs/Lynx) - Show logcat inside the device for debug builds
- [Scalpel](https://github.com/JakeWharton/scalpel) - View the entire hierarchy in 3d in the phone.
- [Stetho](https://github.com/facebook/stetho) - Debug hierarchy and network from chrome.
- [Android Debug Database](https://github.com/amitshekhariitbhu/Android-Debug-Database) - Android Debug Database is a powerful library for debugging databases and shared preferences in Android applications.
- [Android Debug Bridge - ADB](https://github.com/mzlogin/awesome-adb/blob/master/README.en.md) - a command-line tool to assist in debugging Android-powered devices
- [ADB Enhanced](https://github.com/ashishb/adb-enhanced) - a command-line wrapper around ADB for developers, so that, developers don't have to remember esoteric version-dependent commands
- [Pidcat](https://github.com/JakeWharton/pidcat) - a colored command-line ADB wrapper that only shows log entries for a specific application package
- [AppSpector](https://appspector.com) - Remote Android and iOS debugging and data collection service. You can debug networking, logs, SQLite and mock device's geo location.

### Logger
- [logger](https://github.com/orhanobut/logger) - Simple, pretty and powerful logger for android
- [timber](https://github.com/JakeWharton/timber) - A logger with a small, extensible API which provides utility on top of Android's normal Log class.
- [LoggingInterceptor](https://github.com/ihsanbal/LoggingInterceptor) - An OkHttp interceptor which pretty logs request and response data.
- [Bugfender](https://github.com/bugfender/BugfenderSDK-android-sample) - Upload your logs and check them online, specially made for mobile
- [EzyLogger](https://github.com/afiqiqmal/EzyLogger) - Simple Lightweight logger
- [Logback Android](https://github.com/tony19/logback-android) - Logback port to Android which provides a highly configurable logging framework for Android apps.

### Testing

- [Robotium](https://github.com/robotiumtech/robotium) - Test automation framework for black-box UI tests.
- [Roboletric](http://robolectric.org/) - Unit test framework to run tests inside the JVM on your workstation, not in the emulator.
- [AssertJ Android](https://github.com/square/assertj-android) - AssertJ assertions geared towards Android.
- [Green Coffee](https://github.com/mauriciotogneri/green-coffee) - Run your Cucumber tests in your Android instrumentation tests.

### Database
- [Cupboard](https://bitbucket.org/littlerobots/cupboard) - Access the sqlite easily via direct database access or through the ContentProvider framework.
- [DbInspector](https://github.com/infinum/android_dbinspector) - Provides a simple way to view the contents of the in-app database for debugging purposes.
- [SQLite Asset Helper](https://github.com/jgilfelt/android-sqlite-asset-helper) - manage database creation and version management using an application's raw asset files.
- [Realm](https://github.com/realm/realm-java) - The alternative to SQLite and ORMs: Simple, modern and fast! Object oriented API and multi platform support.
- [Realm Asset Helper](https://github.com/eggheadgames/android-realm-asset-helper) - Copies a realm database from the apk assets folder. Efficiently handles versioning of read-only realm databases.
- [RestorableSQLiteDatabase](https://github.com/yaa110/RestorableSQLiteDatabase) - A wrapper to replicate android's SQLiteDatabase with restoring capability.
- [Nitrite Database](https://github.com/dizitart/nitrite-database) - A NoSQL embedded document store for Android with MongoDb like API.

### Dependency Injection

- [Dagger 2](https://github.com/google/dagger) - A fast dependency injector for Android and Java.
- [Butter Knife](http://jakewharton.github.io/butterknife/) - View "injection" library for Android.
- [ActivityStarter](https://github.com/MarcinMoskala/ActivityStarter) - Android Library that provide simpler way to start the Activities with multiple arguments.
- [AndroidAnnotations](https://github.com/androidannotations/androidannotations) - Java annotations with dependency injection at compile time.
- [Toothpick](https://github.com/stephanenicolas/toothpick) - A scope tree based Dependency Injection (DI) library for Java.

### Android Services

- [Remoter](https://github.com/josesamuel/remoter) - An alternative to Android AIDL for Android Remote IPC services using plain java interfaces.
- [Service Connector](https://github.com/josesamuel/serviceconnector) - Bind Android services and callbacks to fields and methods.

### Game Development

- [Libgdx](https://libgdx.badlogicgames.com/) - Cross-platform game engine and SDK. [Open Source](https://github.com/libGDX/libGDX)
- [Vuforia](https://www.vuforia.com/) - Augmented Reality library.
- [Unity](https://unity3d.com/unity/features/multiplatform) - Cross-platform game creation system.
- [Rajawali](https://github.com/Rajawali/Rajawali) - Android OpenGL ES 2.0/3.0 Engine
- [Cocos2d-x](http://www.cocos2d-x.org) - Cross-platform 2d game framework.
- [JustWeEngine](https://github.com/lfkdsk/JustWeEngine) - An easy open source Android Native Game FrameWork.


### Utility

- [Conceal SharedPreferences](https://github.com/afiqiqmal/SharedChamber) - Secured Preferences using Facebook Secure Encryption called Conceal.
- [EventBus](http://greenrobot.github.io/EventBus/) - EventBus is a library that simplifies communication between different parts of your application.
- [Otto](https://github.com/square/otto) - Event Bus for Android.
- [Weak handler](https://github.com/badoo/android-weak-handler) - Memory safer implementation of android.os.Handler.
- [Byte Buddy](http://bytebuddy.net) - Runtime code generation library with support for Android.
- [Secure Preference Manager](https://github.com/prashantsolanki3/Secure-Pref-Manager) - Secure Preference Manager for android. It uses various Encryption to protect your application's Shared Preferences.
- [LeakCanary](https://github.com/square/leakcanary) - Catch memory leaks as they occur.
- [Drekkar](https://github.com/coshx/drekkar) - An Android event bus for WebView and JS.
- [Androl4b](https://github.com/sh4hin/Androl4b) - A vm for assessing android applications.
- [DroidMVP](https://github.com/andrzejchm/DroidMVP) - Android library to help you incorporate MVP along with Passive View and Presentation Model patterns into your app.
- [Gota](https://github.com/alhazmy13/Gota) - Simplifying Android Permissions.
- [EasyDeviceInfo](https://github.com/nisrulz/easydeviceinfo) - Get device information in a super easy way.
- [Ask-Permission](https://github.com/Kishanjvaghela/Ask-Permission) - Simple RunTime permission manager.
- [Shutter-Android](https://github.com/levibostian/Shutter-Android) - Capture photos/videos from device camera or get photos/video from gallery app with no runtime permissions needed.
- [Validator](https://github.com/anderscheow/Validator) - An utilities class to validate text inside TextInputLayout.

### Other

- [Android Support library](https://developer.android.com/topic/libraries/support-library/) - The Android Support Library package is a set of code libraries that provide backward-compatible versions of Android framework API.
- [Google Play Services](https://developers.google.com/android/guides/overview) - Library to access Google services, such as account syncing, Google+ (sharing, single sign-on), Google Maps, Location APIs, Google Play Games, Cloud Messaging, Android Device Manager, and others.
- [Tape](https://github.com/square/tape) - A lightning fast, transactional, file-based FIFO for Android and Java.
- [Guava: Google Core Libraries for Java](https://github.com/google/guava) - Collections, caching, primitives support, concurrency libraries, common annotations, string processing, I/O, and so forth.
- [Android Scripting](https://github.com/damonkohler/sl4a) - Allows to run scripting languages on Android.
- [Android Priority Job Queue](https://github.com/yigit/android-priority-jobqueue) - Implementation of a Job Queue to easily schedule jobs (tasks) that run in the background, improving UX and application stability.
- [RateMeMaybe](https://github.com/nspo/RateMeMaybe) - Asks the user if (s)he wants to open the Play Store to rate your application.
- [Easy Rating Dialog](https://github.com/fernandodev/easy-rating-dialog) - Lib provides a simple way to display an alert dialog for rating app.
- [ZXing Android-Integration](https://github.com/zxing/zxing) - Integration with Barcode Scanner via Intent.
- [Gradle Retrolambda Plugin](https://github.com/evant/gradle-retrolambda) - Java 8 Lambdas on Android!
- [RxJava](https://github.com/ReactiveX/RxJava)- RxJava – Reactive Extensions for the JVM – a library for composing asynchronous and event-based programs using observable sequences for the Java VM.
- [RxBinding](https://github.com/JakeWharton/RxBinding)- RxBinding – RxJava binding APIs for Android UI widgets from the platform and support libraries.
- [Caffeine](https://github.com/percolate/caffeine) - A collection of utility classes that help make Android development faster.
- [AboutLibraries](https://github.com/mikepenz/AboutLibraries) - Automatically generates an About this app section, with a list of used libraries.
- [AudioPlayerView](https://github.com/HugoMatilla/AudioPlayerView) - A view that loads audio from an url and have basic playback tools.
- [andle](https://github.com/Jintin/andle) - command line tool help you sync dependencies, sdk or build tool version.
- [Typography](https://github.com/workarounds/typography) - An Android library that makes it easy to use custom fonts in views.
- [Calligraphy](https://github.com/chrisjenx/Calligraphy) - Custom fonts in Android an OK way.
- [transai](https://github.com/Jintin/transai) - command line tool help you manage localization string files.
- [Android-Link-Preview](https://github.com/LeonardoCardoso/Android-Link-Preview) - It makes a preview from an url, grabbing all the information such as title, relevant texts and images.
- [Sensey](https://github.com/nisrulz/sensey) - Detecting gestures in a snap.
- [UserAwareVideoView](https://github.com/kevalpatel2106/UserAwareVideoView) - A customized video view that will automatically pause video is user is not looking at device screen!
- [Flexbox Layout](https://github.com/google/flexbox-layout) - FlexboxLayout is a library which brings the similar capabilities of CSS Flexible Box Layout Module to Android. 
- [Agile Boiler Plate](https://github.com/xresco/Android-Agile-Boiler-Plate) - The boiler plate is based on MVP architecture and it is fully based on Dependency Injection design pattern using Dagger2.
