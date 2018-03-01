# from 계열의 Operators.

RxJava에서 Observable을 생성하는 함수 중, `just()`와 `create()` 함수는 단일 데이터에 대한 Observable을 생성하는 함수이다.  
단일 데이터가 아닌 경우에는 `fromXXX()` 계열의 함수를 사용하면 된다.

RxJava 1.x 버전에서는 `from()`과 `fromCallable()` 함수만 사용 했었지만, `from()` 함수를 이용하여 배열, 반복자, 비동기 계산 등에 모두 사용하다 보니 모호함이 있었고, RxJava 2.x 버전에 오면서 `from()` 함수를 세분화하였다고 한다.

RxJava 2.x에서 제공되는 from 계열의 함수에는, `fromArray()`, `fromIterable()`, `fromCallable()`, `fromFuture()`, `fromPublisher()` 함수 용도에 맞게 제공한다.

## fromArray() 함수
`fromArray()` 함수는 배열에 들어 있는 데이터를 처리할 때 활용된다.

### \#. Exam Code
``` java
public static void main(String[] args) {
  String[] corps = { "Google", "Apple", "Microsoft" };
  Observable<String> source = Observable.fromArray(corps);
  source.subscribe(System.out::println);
}
```

## fromIterable() 함수
`fromIterable()` 함수는,  
Java의 클래스 중, `Iterable Interface`를 구현한 클래스를 이용하여 Observable을 생성하는 방법이다.  
Java에서 `Iterable Interface`를 구현한 대표적인 클래스로는 `ArrayList`, `HashSet`, `LinkedList` 등이 있다.

### \#. Exam Code
``` java
public static void main(String[] args) {
  List<String> corps = new ArrayList<>();
  corps.add("Google");
  corps.add("Apple");
  corps.add("Microsoft");

  Observable<String> source = Observable.fromIterable(corps);
  source.subscribe(System.out::println);
}
```

## fromCallable() 함수
`fromCallable()` 함수는, Java의 `Callable` 인터페이스 객체를 이용한 Observable 생성 방법이다.

### \#. Exam Code
``` java
public static void main(String[] args) {
  Callable<String> callable = () => {
    Thread.sleep(1000);
    return "Hello, Callable";
  };

  Observable<String> source = Observable.fromCallable(callable);
  source.subscribe(System.out::println);
}
```

## fromFuture() 함수
`fromFuture()` 함수는, Java의 `Future` 인터페이스 객체를 이용한 Observable 생성 방법이다.  
보통 `Executor` 인터페이스를 구현한 클래스에 `Callable` 객체를 인자로 넣어 `Future` 객체를 반환한다.

### \#. Exam Code
``` java
public static void main(String[] args) {
  Future<String> future = Executors.newSingleThreadExecutor().submit(() => {
    Thread.sleep(1000);
    return "Hello, Future";
  });

  Observable<String> source = Observable.fromFuture(future);
  source.subscribe(System.out::println);
}
```

## fromPublisher() 함수
`fromPublisher()` 함수는, **Java9**의 Flow API 일부인 `Publisher` 인터페이스 객체를 이용한 Observable 생성 방법이다.  
`Publisher` 인터페이스 객체는 `create()` 함수와 마찬가지로 `onNext()`, `onComplete()` 함수를 호출할 수 있다.

### \#. Exam Code
``` java
public static void main(String[] args) {
  Publisher<String> publisher = (Subscriber<? super String> s) -> {
    s.onNext("Hello, Publisher");
    s.onComplete();
  };

  Observable<String> source = Observable.fromPublisher(publisher);
  source.subscirbe(System.out::println);
}
```


[marble-diagram]: http://reactivex.io/documentation/operators/images/from.c.png