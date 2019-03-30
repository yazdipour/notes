# Android

## Amazing open source Android apps

https://github.com/Mybridge/amazing-android-apps/blob/master/README.md

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

## DB

* KeyValue: SnappyDB
* ORM: ActiveAndroid, SugarORM, DBFlow

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