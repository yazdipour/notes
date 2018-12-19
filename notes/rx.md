# Rx

## RxPy

```python
from rx import Observable
somelist=[1,2,3]
def do_obs(observer):
	for x in somelist:
		if(x==2): observer.on_error(x)
		else: observer.on_next(x)
	observer.on_completed()

source = Observable.create(do_obs)
source.subscribe(on_next=lambda value: print("next_{0}".format(value)),
	on_error=lambda: print("completed"),
	on_completed=lambda r: print("error_{0}".format(r)))
```

## RxJava

* https://github.com/ReactiveX/RxJava/wiki
* https://github.com/ReactiveX/RxAndroid/wiki
* https://github.com/kaushikgopal/RxJava-Android-Samples
* [**RxJava: Alphabetical List of Observable Operators**](https://github.com/ReactiveX/RxJava/wiki/Alphabetical-List-of-Observable-Operators)
* [**Pro Presentaion + Slides: The State of Managing State with RxJava**](https://jakewharton.com/the-state-of-managing-state-with-rxjava/)

* [**Excellent Slides + Diagram of functions + Android Examples**](http://slides.com/yaroslavheriatovych/frponandroid#/)

* [**Excellent Slides + Diagram of functions + Android Examples_2**](http://slides.com/yaroslavheriatovych/rxtips-3#/)

### Observable transformation

* `map( )` — transform the items emitted by an Observable by applying a function to each of them 
* `flatMap( )` — transform the items emitted by an Observable into Observables, then flatten this into a single Observable 
* `scan( )` — apply a function to each item emitted by an Observable, sequentially, and emit each successive value 
* `groupBy( )` and groupByUntil( ) — divide an Observable into a set of Observables that emit groups of items from the original Observable, organized by key 
* `buffer( )` — periodically gather items from an Observable into bundles and emit these bundles rather than emitting the items one at a time 
* `window( )` — periodically subdivide items from an Observable into Observable windows and emit these windows rather than emitting the items one at a time 

### Observable filtering

filter( ) — filter items emitted by an Observable
takeLast( ) — only emit the last n items emitted by an Observable
takeLastBuffer( ) — emit the last n items emitted by an Observable, as a single list item
skip( ) — ignore the first n items emitted by an Observable
take( ) — emit only the first n items emitted by an Observable
first( ) — emit only the first item emitted by an Observable, or the first item that meets some condition
elementAt( ) — emit item n emitted by the source Observable
timeout( ) — emit items from a source Observable, but issue an exception if no item is emitted in a specified timespan
distinct( ) — suppress duplicate items emitted by the source Observable

### _ 

An `Observable` emits items; a `Subscriber` consumes those items.

```java
//simple
Observable.just("Hello, world!").subscribe(onNextAction, onErrorAction_optional, onCompleteAction_optional);

Subscriber<String> subscriber = new Subscriber<String>(){
    @Override
    public void onCompleted(){/*print Complete*/}
    @Override
    public void onError(Throwable t){/*print Error*/}
    @Override
    public void onNext(String s){/*do things with 's'*/}
};
Observable.from(new ArrayList<String>("A","B"))
    .filter(x->x.startsWith("A"))
    .subscribe(subscriber);
```

### map

```java
Observable.just("Hello, world!", "Halo!")
    .map(s -> s.hashCode())//map() operator can be used to transform one emitted item into another: like here, from String to Integer
    .map(i -> Integer.toString(i))
    .subscribe(s -> System.out.println(s));
```

### flatMap, filter, take, doOnNext

```java 
Observable<List<String>> query(String text);// Returns a List of website URLs based on a text search
Observable<String> getTitle(String URL);// Returns the title of a website, or null if 404

query("Hello, world!")
    .flatMap(urls -> Observable.from(urls))
    .flatMap(url -> getTitle(url)) //flatMap() is weird, right? Why is it returning another Observable? The key concept here is that the new Observable returned is what the Subscriber sees. It doesn't receive a List<String> - it gets a series of individual Strings as returned by Observable.from().
    .filter(title -> title != null) //filter() emits the same item it received, but only if it passes the boolean check.
    .take(5)//take() emits, at most, the number of items specified. 
    .doOnNext(title -> saveTitle(title))//doOnNext() allows us to add extra behavior each time an item is emitted, in this case saving the title.
    .subscribe(title -> System.out.println(title));
```

### Thread

```java
myObservableServices.retrieveImage(url)
    .subscribeOn(Schedulers.io())
    .observeOn(AndroidSchedulers.mainThread())//which thread to run on using subscribeOn(), and which thread your Subscriber should run on using observeOn(). How simple is that? Everything that runs before my Subscriber runs on an I/O thread. Then in the end, my View manipulation happens on the main thread.
    .subscribe(bitmap -> myImageView.setImageBitmap(bitmap));
```

### Subscription

```java
Subscription subscription = Observable.just("Hello, World!")
    .subscribe(s -> System.out.println(s));
subscription.unsubscribe();
System.out.println("Unsubscribed=" + subscription.isUnsubscribed());
```

## RxAndroid

* `AndroidSchedulers` which provides schedulers ready-made for Android's threading system.

```java
retrofitService.getImage(url)
    .subscribeOn(Schedulers.io())
    .observeOn(AndroidSchedulers.mainThread())
    .subscribe(bitmap -> myImageView.setImageBitmap(bitmap));
```

* `AndroidObservable` which provides more facilities for working within the Android lifecycle. There is bindActivity() and bindFragment() which, in addition to automatically using AndroidSchedulers.mainThread() for observing, will also stop emitting items when your Activity or Fragment is finishing.

```java
AndroidObservable.bindActivity(this, retrofitService.getImage(url))
    .subscribeOn(Schedulers.io())
    .subscribe(bitmap -> myImageView.setImageBitmap(bitmap));
```

* `AndroidObservable.fromBroadcast()`, which allows you to create an Observable that works like a BroadcastReceiver. Here's a way to be notified whenever network connectivity changes.

```java
IntentFilter filter = new IntentFilter(ConnectivityManager.CONNECTIVITY_ACTION);
AndroidObservable.fromBroadcast(context, filter)
    .subscribe(intent -> handleConnectivityChange(intent));
```

* `ViewObservable`, which adds a couple bindings for Views. There's ViewObservable.clicks() if you want to get an event each time a View is clicked, or ViewObservable.text() to observe whenever a TextView changes its content.

```java
ViewObservable.clicks(mCardNameEditText, false)
    .subscribe(view -> handleClick(view));
```

### Retrofit

* Now not only will you get your data but you can transform it, too!

```java
@GET("/user/{id}/photo")
Observable<Photo> getUserPhoto(@Path("id") int id);
```

* makes it easy to combine multiple REST calls together.

```java
Observable.zip(
    service.getUserPhoto(id),
    service.getPhotoMetadata(id),
    (photo, metadata) -> createPhotoWithData(photo, metadata))
    .subscribe(photoWithData -> showPhoto(photoWithData));
```

### Memory leaks

The first problem can be solved with some of RxJava's built-in caching mechanisms, so that you can unsubscribe/resubscribe to the same Observable without it duplicating its work. In particular, cache() (or replay()) will continue the underlying request (even if you unsubscribe). That means you can resume with a new subscription after Activity recreation:

```java
Observable<Photo> request = service.getUserPhoto(id).cache();
Subscription sub = request.subscribe(photo -> handleUserPhoto(photo));

// ...When the Activity is being recreated...
sub.unsubscribe();

// ...Once the Activity is recreated...
request.subscribe(photo -> handleUserPhoto(photo));
```

The second problem can be solved by properly unsubscribing from your subscriptions in accordance with the lifecycle. It is a common pattern to use a CompositeSubscription to hold all of your Subscriptions, and then unsubscribe all at once in onDestroy() or onDestroyView():


```java
private CompositeSubscription mCompositeSubscription
    = new CompositeSubscription();

private void doSomething() {
    mCompositeSubscription.add(
        AndroidObservable.bindActivity(this, Observable.just("Hello, World!"))
        .subscribe(s -> System.out.println(s)));
}

@Override
protected void onDestroy() {
    super.onDestroy();
    
    mCompositeSubscription.unsubscribe();
}
```
For bonus points you can create a root Activity/Fragment that comes with a CompositeSubscription that you can add to and is later automatically unsubscribed.
A warning! Once you call CompositeSubscription.unsubscribe() the object is unusable, as it will automatically unsubscribe anything you add to it afterwards! You must create a new CompositeSubscription as a replacement if you plan on re-using this pattern later.

