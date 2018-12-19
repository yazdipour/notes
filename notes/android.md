# Android

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