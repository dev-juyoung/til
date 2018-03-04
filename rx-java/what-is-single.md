# Single 클래스

Single 클래스는 RxJava 1.x 버전부터 존재하던 Observable의 특수한 형태이다.  
Observable 클래스는 데이터를 무한하게 발행 할 수 있지만, Single 클래스는 오직 1개의 데이터만 발행하도록 한정된다.  
일반적으로, 결과가 유일한 서버 API를 호출할 때 유용하게 사용할 수 있다.

### \#. Marble Diagram
![Marble Diagram][marble-diagram]

해당 마블다이어그램에서 중요하게 보아야 할 점은, 데이터가 발행됨과 동시에 종료된다는 점이다.

일반적인 Observable의 라이프사이클은 `onNext()`함수와 `onComplete()` 함수가 분리되어 있으나, Single 클래스는 `onSuccess()` 함수로 두 형태가 통합된 것이다.

그러므로, Single 클래스에는 `onSuccess()` 함수와 `onError()` 함수로 구성된다.

### \#. Exam Code 
``` java
public static void main(String[] args) {
  Single<String> source = Single.just('Hello, Single');
  source.subscribe(System.out::println);
}
```

### \#. Observable에서 Single 클래스 이용

Single 클래스는 Observable의 특수한 형태이므로 기존의 Observable 클래스에서 변환이 가능하다.

### \#. Exam Code
``` java
public static void main(String[] args) {
  // Case1.
  Observable<String> source = Observable.just("Hello, Single");
  Single.fromObservable(source).subscribe(System.out::println);

  // Case2.
  Observable.just("Hello, Single")
            .single("default value")
            .subscribe(System.out::println);

  // Case3.
  String[] colors = { "RED", "GREEN", "BLUE" };
  Observable.fromArray(color)
            .first("YELLOW")
            .subscribe(System.out::println);

  // Case4.
  Observable.empty()
            .single("default value")
            .subscribe(System.out::println);

  // Case5.
  Observable.just("Google", "Apple", "Microsoft")
            .take(1)
            .single("Empty Company")
            .subscribe(System.out::println);
}
```

위의 예제코드를 하나씩 해석해보면 다음과 같다.
* Case1.
  > 기존의 Observable 객체에서 Single 객체로 변환.
* Case2.
  > `single()` 함수를 이용하여 Single 객체를 생성.  
  > `single()` 함수는 인자로 기본값을 가질 수 있다.
* Case3.
  > `first()` 함수를 이용하여 Single 객체를 생성.  
  > `single()` 객체와 마찬가지로 인자로 기본값을 가질 수 있다.  
  > **`first()` 함수는 하나 이상의 데이터를 발행하더라도 첫 번째 데이터만 발행 한 후 onSuccess() 이벤트가 호출된다.**
* Case4.
  > `Empty Observable` 에서 Single 객체를 생성.
* Case5.
  > `take()` 함수를 이용하여 Single 객체를 생성.

[marble-diagram]: https://raw.github.com/wiki/ReactiveX/RxJava/images/rx-operators/Single.legend.png