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

## Fastlane

```shell
fastlane init
# modify fastlane file
fastlane android deploy
```