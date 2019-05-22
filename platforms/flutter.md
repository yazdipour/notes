# flutter

- https://flutterstudio.app/
- https://pub.dartlang.org/flutter
- http://fluttericon.com/
- http://mutisya.com/
- https://startflutter.com/

## Flutter for Xamarin.Forms developers

https://flutter.dev/docs/get-started/flutter-for/xamarin-forms-devs

## How to sign Flutter apps for iOS automatically without a Mac

https://blog.codemagic.io/automatic-code-signing-for-ios-that-doesnt-require-a-mac/

## Async

```dart
Import 'dart:async';
Future<bool> foo() async{}

Var x=await foo();

Foo().then( (int x){…} //func run after that );

Future f1= foo();
Future f2= foo();
Future f3= foo();
Await Future.wait([f1,f2,f3]);
```