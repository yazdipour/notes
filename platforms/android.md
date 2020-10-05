# Android

- Realm: https://virgool.io/@sjd.noroozi91/بلعیدن-شیرینی-دانمارکی-یا-راهکاری-برای-قورت-دادن-استوانه-ها-mcftjpolptjs
- KeyValue: SnappyDB
- ORM: ActiveAndroid, SugarORM, DBFlow
- ROOM: https://programchi.ir/2018/08/27/آموزش-دیتابیس-room-در-اندروید/
- Drawer: https://programchi.ir/2018/04/05/آموزش-navigation-drawer-متریال-دیزاین-در-اندروید/
- SQLITE Lazy: https://dmytrodanylyk.com/articles/lazy-sqlite/
- Deep Link: https://programchi.ir/2018/04/06/آموزش-deep-link-در-برنامه-نویسی-اندروید/
- espresso: https://programchi.ir/2018/08/12/آموزش-espresso-در-برنامه-نویسی-اندروید/

## SSL OkHttp

```java
X509TrustManager trustManager;
SSLSocketFactory sslSocketFactory;
CustomTrust customTrust = new CustomTrust();
trustManager = customTrust.getTrustManager();
sslSocketFactory = customTrust.getSslSocketFactory();
OkHttpClient.Builder httpClient = new OkHttpClient.Builder()
                .connectTimeout(timeOut, TimeUnit.SECONDS)
                .readTimeout(timeOut, TimeUnit.SECONDS)
                .sslSocketFactory(sslSocketFactory, trustManager)
                .hostnameVerifier((s, sslSession) -> true)
                .writeTimeout(timeOut, TimeUnit.SECONDS);
if (BuildConfig.DEBUG) HttpLoggingInterceptor loggingInterceptor = new HttpLoggingInterceptor();
```

## LruCache

```java
int availableBytes = ((ActivityManager)getSystemService(Context.ACTIVITY_SERVICE)).getMemoryClass() * 1024 * 1024 / 8;
LruCache bitmapCache = new LruCache<String, Bitmap>(availableBytes);
```

## Speedup Gradle

[Gradle Speedup](assets/android/speedup-gradle.pdf)

## Instant

![instant](assets/android/instant.png)

## Hide Keyboard

```java
InputMethodManagermgr=(InputMethodManager)getSystemService(Context.INPUT_METHOD_SERVICE);
mgr.hideSoftInputFromWindow(edit,0);
```

## Make NestedScrollView full

Add `android:fillViewport="true"` to NestedScrollView

## Amazing open source Android apps

- https://github.com/Mybridge/amazing-android-apps/blob/master/README.md

## Anotations

```java
String getString(@StringRes int id) { return context.getString(id); }
```

## Manifest

### android:networkSecurityConfig

Specifies the name of the XML file that contains your application's Network Security Configuration. The value must be a reference to the XML resource file containing the configuration. This attribute was added in API level 24.

### android:persistent

Whether or not the application should remain running at all times — "true" if it should, and "false" if not. The default value is "false". Applications should not normally set this flag; persistence mode is intended only for certain sys

### android:largeHeap

Whether your application's processes should be created with a large Dalvik heap. This applies to all processes created for the application. It only applies to the first application loaded into a process; if you're using a shared user ID to allow multiple applications to use a process, they all must use this option consistently or they will have unpredictable results.

### android:hardwareAccelerated

Whether or not hardware-accelerated rendering should be enabled for all activities and views in this application — "true" if it should be enabled, and "false" if not. The default value is "true" if you've set either minSdkVersion or targetSdkVersion to "14" or higher; otherwise, it's "false".

### IntentFilter

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

## Lifecycle

• Fragment
○ onAttach
○ onCreate
○ onCreateView
○ onActivityCreated
○ onStart
○ onResume
○ onPause
○ onDestroyView
○ onDestroy
○ onDetach
• Activity
○ onCreate
○ onStart
○ onResume
○ onPause
○ onStop
○ onDestroy
○ onRestart

## MVVM

### Life-cycle

- Lifecycle: an object that defines an Android Lifecycle
- LifecycleOwner: an interface for objects with a Lifecycle

  - `getLifecycle()`
  - AppCompatActivity / Fragment
    `Lifecycle.isAtLeast(Lifecycle.State.STARTED)`
  - ProcessLifecycleOwner
  - LifecycleService

  ```java
  class MyObserver: DefaultLifecycleObserver{
      override fun onResume(owner:LifecycleOwner){}
      override fun onPause(owner:LifecycleOwner){}
  }

  // Activity / Fragment observer
  lifecycle.addObserver(MyObserver())
  // process observer
  ProcessLifecycleOwner.get().lifecycle.addObserver(MyObserver())
  // service observer
  myLifecycleService.lifecycle.addObserver(MyObserver())
  ```

- LifecycleObserver: an interface for observing a Lifecycle

### ViewModel

```kt
class UserProfileViewModel: ViewModel(){
    private val _user = MutableLiveData<User>()
    val user : LiveData<User>
        get() = _user
}
```

- We should use `LiveData` for Views and `MutableLiveData` in ViewModel side.

```java
private MutableLiveData<String> mCurrentName;
public LiveData<String> getCurrentName(){
	if(mCurrentName==null)mCurrentName=new MutableLiveData<String>();
	return mCurrentName;
```

### View

```kt
override fun onCreate(savedInstanceState: Bundle?){
    val userViewModel = ViewModelProviders.of(this).get(UserProfileViewModel::class.java)

    val binding = ActivityMainBinding.inflate(layoutInflater)
    binding.viewmodel = userViewModel
    binding.setLifecycleOwner(this)
    setContentView(binding.root)

}
// Meanwhile in another Component
user.setValue(newUser)  // UI Thread
user.postValue(newUser) // Bg Thread
```

```java
// onCreate(){
userViewModel = ViewModelProviders.of(this).get(.class);
userViewModel.init();
userViewModel.getCurrentName().observe(this,
    new Observer<List<String>>(){
        @Override public void onChanged(@Nullable List<String> mList){
            adapter.notifyDataSetChanged();
        }
});
```

### Binding

```kt
//onChanged() will trigger this
userViewModel.user.observe(this,Observer{user->userNameTextView.text = user?.name})
```

OR

```xml
<layout>
    <data>
        <variable name="viewmodel" type="android.example.com.UserProfileViewModel"/>
    </data>
    <TextView android:text="@{viewmodel.user.name}"/>
```

### Transforming LiveData

- `map()` apply function to change LiveData output

  ```kt
  //in vm
  var userNameLiveData = Transformations.map(userLiveData{user->"${user.name} ${user.lastname"})
  ```

- `switchMap()` apply function that swaps LiveData observer is listening to. (Like Searching, Loged in User)

  ```ky
  val userNamesResult: LiveData<Result> = Transformations.switchMap(query, resposity.search(it))
  ```

- `MediatorLiveData`: custom transformations

## RX

```java
boolean ready = false;
Observable<Boolean> observable = Observable.just(ready);
// Observer<Boolean> observer = new Observer<Boolean>() {
DisposableObserver observer = new DisposableObserver<Boolean>() {
    @Override
    public void onSubscribe(Disposable d) {
        // When someone subscibes
    }

    @Override
    public void onNext(Boolean aBoolean) {
        // When NEXT comes
    }

    @Override
    public void onError(Throwable e) {
        // When NEXT is error
    }

    @Override
    public void onComplete() {
        // When there is no NEXT
    }
};
observable.subscribe(observer);
// if is DisposableObserver
observer.dispose();
```

### Rx Source

```java
Flowable.fromCallable(()->"H");
Observable.fromCallable(()->"H");
Single.fromCallable(()->"H");

Maybe.fromCallable(()->"H");
Maybe.fromAction(()->System.out.print("H"));
Maybe.fromRunnable(()->System.out.print("H"));

Completable.fromCallable(()->"H");
Completable.fromAction(()->System.out.print("H"));
Completable.fromRunnable(()->System.out.print("H"));
```

### Rx Retrofit

```java
@POST("/login")
@FormUrlEncode
Observable<String> login(@Field("username") String user);
```

### Rx Okhttp

```java
OkHttpClient client;
Request requet;
Observable.fromCallable(new Callable<String>(){
    @Override public String call() throw Exception{
        return client.newCall(request).execute();
    }
});
```

### Rx Binding (SearchTextView)

```java
RxTextView.textChanges(search_tv)
    .filter(s -> s.length() >2)
    .debounce(100, TimeUnit.MILLISECONDS)
    .flatMap(s -> makeApiCall(s))
    .subscribOn(Schedulers.io())
    .observeOn(AndroidSchedulers.mainThread())
    .subscribe(observer);
```

## Caching Retrofit

https://medium.com/mindorks/caching-with-retrofit-store-responses-offline-71439ed32fda

## Retrofit Maintain Cookie Session

`compile ‘com.squareup.okhttp3:okhttp-urlconnection:3.6.0’`

```java
CookieHandler cookieHandler = new CookieManager();
okHttpClient.cookieJar(new JavaNetCookieJar(cookieHandler));
```

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
mSocket.emit("new message", message); //Emitting events * Sending data
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
        <variable name="vm" type="com.example.vm"/>
    </data>

    <TextView
    android:visibility="@{bool1? View.VISIBLE:View.GONE}"
    android:text="@{@string/pFormat{p.Name}}"
    android:text2="@={p.Age, default=my_default}"
    app:onRefreshListener="@{() -> vm.refreshList()}"
    android:onClick="@{() -> vm.onClickedCellAt(0, 0)}"
    android:text='@{vm.arr["00"]}'
    />
```

### Test Rx Mockito

```java
@Test
public void testGetImage(){
    Mockito.when(mDataModel.getGreeting()).thenReturn(Observable.just("Hello"));
    TestSubscriber<Integer> testSubscriber = new TestSubscriber();
    mViewModel.getImage().subscribe(testSubscriber);
    testSubscriber.assertNoValues();
}
```

## Resources

- https://androidresources.net/
- [Libraries](https://android-arsenal.com/)
- [Libraries⭐](https://fossdroid.com)
- [Svg2Drawable](http://inloop.github.io/svg2android/)
- [OneSignal](https://onesignal.com/apps/8e8fc011-b4da-4d3f-88ec-f170bcddd292)
- [Farsi Tutorial](https://programchi.ir/)
- [Tutorial Futurestud](https://futurestud.io/)
- https://material.io/icons/#ic_done
- https://romannurik.github.io/AndroidAssetStudio/index.html

### Kotlin

- https://kotlin.link/?q=%20
- https://hackr.io/tutorials/learn-kotlin

### Animations

- [Rebound](https://github.com/facebook/rebound) \* Rebound is a Java library that models spring dynamics.
- [Android View Animations](https://github.com/daimajia/AndroidViewAnimations) \* Cute view animation collection.
- [Android-Transition](https://github.com/kaichunlin/android-transition) \* Allows the easy creation of view transitions that react to user inputs.
- [Android-View-Actions](https://github.com/dtx12/AndroidAnimationsActions) \* Makes creating complex animations for views easy.
- [Swipper](https://github.com/mdg-iitr/Swipper) \* Android library for swipeable gestures to control volume , brightness and seek .
- [Spotlight](https://github.com/TakuSemba/Spotlight) \* Android Library that lights items for tutorials or walk-throughs etc...

### Security

- [libsignal-protocol-java](https://github.com/signalapp/libsignal-protocol-java) \* A ratcheting forward secrecy protocol that works in synchronous and asynchronous messaging environments.
- [Themis](https://github.com/cossacklabs/themis) \* Multi-language framework for making typical encryption schemes easy to use: data at rest, authenticated data exchange, transport protection, authentication, and so on.

### Date & Time

- [ThreeTen Android Backport](https://github.com/JakeWharton/ThreeTenABP) \* An adaptation of the JSR-310 backport for Android.
- [Joda-Time Android](https://github.com/dlew/joda-time-android) \* Joda-Time library with Android specialization.
- [True Time](https://github.com/instacart/truetime-android) \* Android NTP time library. Get the true current time impervious to device clock time changes.

### Runtime Permissions

- [Permission Dispatcher](https://github.com/permissions-dispatcher/PermissionsDispatcher) \* Simple annotation-based API to handle runtime permissions.
- [RxPermissions](https://github.com/tbruyelle/RxPermissions) \* Android runtime permissions powered by RxJava.
- [NoPermission](https://github.com/NoNews/NoPermission) \* Simple Android library for permissions request. Consists of only one class.

### Debugging Tools

- [Linx](https://github.com/pedrovgs/Lynx) \* Show logcat inside the device for debug builds
- [Scalpel](https://github.com/JakeWharton/scalpel) \* View the entire hierarchy in 3d in the phone.
- [Stetho](https://github.com/facebook/stetho)

  - Debug hierarchy and network from Chrome DevTools.
  - Network Inspection
  - Database Inspection
  - View Hierarchy
  - dumpapp
  - Javascript Console
  - https://youtu.be/iyXpdkqBsG8

- [Android Debug Database](https://github.com/amitshekhariitbhu/Android-Debug-Database) \* Android Debug Database is a powerful library for debugging databases and shared preferences in Android applications.
- [Android Debug Bridge \* ADB](https://github.com/mzlogin/awesome-adb/blob/master/README.en.md) \* a command-line tool to assist in debugging Android-powered devices
- [ADB Enhanced](https://github.com/ashishb/adb-enhanced) \* a command-line wrapper around ADB for developers, so that, developers don't have to remember esoteric version-dependent commands
- [Pidcat](https://github.com/JakeWharton/pidcat) \* a colored command-line ADB wrapper that only shows log entries for a specific application package
- [AppSpector](https://appspector.com) \* Remote Android and iOS debugging and data collection service. You can debug networking, logs, SQLite and mock device's geo location.

### Logger

- [logger](https://github.com/orhanobut/logger) \* Simple, pretty and powerful logger for android
- [timber](https://github.com/JakeWharton/timber) \* A logger with a small, extensible API which provides utility on top of Android's normal Log class.
- [LoggingInterceptor](https://github.com/ihsanbal/LoggingInterceptor) \* An OkHttp interceptor which pretty logs request and response data.
- [Bugfender](https://github.com/bugfender/BugfenderSDK-android-sample) \* Upload your logs and check them online, specially made for mobile
- [EzyLogger](https://github.com/afiqiqmal/EzyLogger) \* Simple Lightweight logger
- [Logback Android](https://github.com/tony19/logback-android) \* Logback port to Android which provides a highly configurable logging framework for Android apps.

### Testing

- [Robotium](https://github.com/robotiumtech/robotium) \* Test automation framework for black-box UI tests.
- [Roboletric](http://robolectric.org/) \* Unit test framework to run tests inside the JVM on your workstation, not in the emulator.
- [AssertJ Android](https://github.com/square/assertj-android) \* AssertJ assertions geared towards Android.
- [Green Coffee](https://github.com/mauriciotogneri/green-coffee) \* Run your Cucumber tests in your Android instrumentation tests.

### Database

- [Cupboard](https://bitbucket.org/littlerobots/cupboard) \* Access the sqlite easily via direct database access or through the ContentProvider framework.
- [DbInspector](https://github.com/infinum/android_dbinspector) \* Provides a simple way to view the contents of the in-app database for debugging purposes.
- [SQLite Asset Helper](https://github.com/jgilfelt/android-sqlite-asset-helper) \* manage database creation and version management using an application's raw asset files.
- [Realm](https://github.com/realm/realm-java) \* The alternative to SQLite and ORMs: Simple, modern and fast! Object oriented API and multi platform support.
- [Realm Asset Helper](https://github.com/eggheadgames/android-realm-asset-helper) \* Copies a realm database from the apk assets folder. Efficiently handles versioning of read-only realm databases.
- [RestorableSQLiteDatabase](https://github.com/yaa110/RestorableSQLiteDatabase) \* A wrapper to replicate android's SQLiteDatabase with restoring capability.
- [Nitrite Database](https://github.com/dizitart/nitrite-database) \* A NoSQL embedded document store for Android with MongoDb like API.

### Dependency Injection

- [Dagger 2](https://github.com/google/dagger) \* A fast dependency injector for Android and Java.
- [Butter Knife](http://jakewharton.github.io/butterknife/) \* View "injection" library for Android.
- [ActivityStarter](https://github.com/MarcinMoskala/ActivityStarter) \* Android Library that provide simpler way to start the Activities with multiple arguments.
- [AndroidAnnotations](https://github.com/androidannotations/androidannotations) \* Java annotations with dependency injection at compile time.
- [Toothpick](https://github.com/stephanenicolas/toothpick) \* A scope tree based Dependency Injection (DI) library for Java.

### Android Services

- [Remoter](https://github.com/josesamuel/remoter) \* An alternative to Android AIDL for Android Remote IPC services using plain java interfaces.
- [Service Connector](https://github.com/josesamuel/serviceconnector) \* Bind Android services and callbacks to fields and methods.

### Game Development

- [Libgdx](https://libgdx.badlogicgames.com/) \* Cross-platform game engine and SDK. [Open Source](https://github.com/libGDX/libGDX)
- [Vuforia](https://www.vuforia.com/) \* Augmented Reality library.
- [Unity](https://unity3d.com/unity/features/multiplatform) \* Cross-platform game creation system.
- [Rajawali](https://github.com/Rajawali/Rajawali) \* Android OpenGL ES 2.0/3.0 Engine
- [Cocos2d-x](http://www.cocos2d-x.org) \* Cross-platform 2d game framework.
- [JustWeEngine](https://github.com/lfkdsk/JustWeEngine) \* An easy open source Android Native Game FrameWork.

### Utility

- [Conceal SharedPreferences](https://github.com/afiqiqmal/SharedChamber) \* Secured Preferences using Facebook Secure Encryption called Conceal.
- [EventBus](http://greenrobot.github.io/EventBus/) \* EventBus is a library that simplifies communication between different parts of your application.
- [Otto](https://github.com/square/otto) \* Event Bus for Android.
- [Weak handler](https://github.com/badoo/android-weak-handler) \* Memory safer implementation of android.os.Handler.
- [Byte Buddy](http://bytebuddy.net) \* Runtime code generation library with support for Android.
- [Secure Preference Manager](https://github.com/prashantsolanki3/Secure-Pref-Manager) \* Secure Preference Manager for android. It uses various Encryption to protect your application's Shared Preferences.
- [LeakCanary](https://github.com/square/leakcanary) \* Catch memory leaks as they occur.
- [Drekkar](https://github.com/coshx/drekkar) \* An Android event bus for WebView and JS.
- [Androl4b](https://github.com/sh4hin/Androl4b) \* A vm for assessing android applications.
- [DroidMVP](https://github.com/andrzejchm/DroidMVP) \* Android library to help you incorporate MVP along with Passive View and Presentation Model patterns into your app.
- [Gota](https://github.com/alhazmy13/Gota) \* Simplifying Android Permissions.
- [EasyDeviceInfo](https://github.com/nisrulz/easydeviceinfo) \* Get device information in a super easy way.
- [Ask-Permission](https://github.com/Kishanjvaghela/Ask-Permission) \* Simple RunTime permission manager.
- [Shutter-Android](https://github.com/levibostian/Shutter-Android) \* Capture photos/videos from device camera or get photos/video from gallery app with no runtime permissions needed.
- [Validator](https://github.com/anderscheow/Validator) \* An utilities class to validate text inside TextInputLayout.

### Other

- [Android Support library](https://developer.android.com/topic/libraries/support-library/) \* The Android Support Library package is a set of code libraries that provide backward-compatible versions of Android framework API.
- [Google Play Services](https://developers.google.com/android/guides/overview) \* Library to access Google services, such as account syncing, Google+ (sharing, single sign-on), Google Maps, Location APIs, Google Play Games, Cloud Messaging, Android Device Manager, and others.
- [Tape](https://github.com/square/tape) \* A lightning fast, transactional, file-based FIFO for Android and Java.
- [Guava: Google Core Libraries for Java](https://github.com/google/guava) \* Collections, caching, primitives support, concurrency libraries, common annotations, string processing, I/O, and so forth.
- [Android Scripting](https://github.com/damonkohler/sl4a) \* Allows to run scripting languages on Android.
- [Android Priority Job Queue](https://github.com/yigit/android-priority-jobqueue) \* Implementation of a Job Queue to easily schedule jobs (tasks) that run in the background, improving UX and application stability.
- [RateMeMaybe](https://github.com/nspo/RateMeMaybe) \* Asks the user if (s)he wants to open the Play Store to rate your application.
- [Easy Rating Dialog](https://github.com/fernandodev/easy-rating-dialog) \* Lib provides a simple way to display an alert dialog for rating app.
- [ZXing Android-Integration](https://github.com/zxing/zxing) \* Integration with Barcode Scanner via Intent.
- [Gradle Retrolambda Plugin](https://github.com/evant/gradle-retrolambda) \* Java 8 Lambdas on Android!
- [RxJava](https://github.com/ReactiveX/RxJava)\* RxJava – Reactive Extensions for the JVM – a library for composing asynchronous and event-based programs using observable sequences for the Java VM.
- [RxBinding](https://github.com/JakeWharton/RxBinding)\* RxBinding – RxJava binding APIs for Android UI widgets from the platform and support libraries.
- [Caffeine](https://github.com/percolate/caffeine) \* A collection of utility classes that help make Android development faster.
- [AboutLibraries](https://github.com/mikepenz/AboutLibraries) \* Automatically generates an About this app section, with a list of used libraries.
- [AudioPlayerView](https://github.com/HugoMatilla/AudioPlayerView) \* A view that loads audio from an url and have basic playback tools.
- [andle](https://github.com/Jintin/andle) \* command line tool help you sync dependencies, sdk or build tool version.
- [Typography](https://github.com/workarounds/typography) \* An Android library that makes it easy to use custom fonts in views.
- [Calligraphy](https://github.com/chrisjenx/Calligraphy) \* Custom fonts in Android an OK way.
- [transai](https://github.com/Jintin/transai) \* command line tool help you manage localization string files.
- [Android-Link-Preview](https://github.com/LeonardoCardoso/Android-Link-Preview) \* It makes a preview from an url, grabbing all the information such as title, relevant texts and images.
- [Sensey](https://github.com/nisrulz/sensey) \* Detecting gestures in a snap.
- [UserAwareVideoView](https://github.com/kevalpatel2106/UserAwareVideoView) \* A customized video view that will automatically pause video is user is not looking at device screen!
- [Flexbox Layout](https://github.com/google/flexbox-layout) \* FlexboxLayout is a library which brings the similar capabilities of CSS Flexible Box Layout Module to Android.
- [Agile Boiler Plate](https://github.com/xresco/Android-Agile-Boiler-Plate) \* The boiler plate is based on MVP architecture and it is fully based on Dependency Injection design pattern using Dagger2.
