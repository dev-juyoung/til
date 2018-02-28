# create() 함수

`create()` 함수는 RxJava의 Operator중 하나이며, `create()` 함수를 이용하여 Observable을 생성 할 경우,  
개발자가 상황에 맞게 `onNext()`, `onError()`, `onComplete()` 알림을 직접 호출해주어야 한다.

하지만, `create()` 함수 대신에, 다른 팩토리 함수를 활용하면 동일할 효과를 낼 수 있기 때문에, `create()` 함수는 RxJava에 익숙한 사용자만 활용하도록 권고한다고 한다.

그래도, `create()` 함수를 사용하여 Observable을 생성할 경우, 몇가지 주의점이 있다.
* Observable이 구독해지 되었을 때, 등록된 콜백을 모두 해제하여야 한다. 그렇지 않을 경우 memory leak이 발생한다.
* 구독자가 구독하는 동안에만 `onNext()`와 `onComplete()` 이벤트를 호출해야 한다.
* 에러 발생 시, `onError()` 이벤트로만 에러를 전달하여야 한다.
* back pressure를 직접 처리해야 한다.

### \#. Marble Diagram
![Marble Diagram][marble-diagram]

* `onNext()` 이벤트를 전달하여 빨간원 데이터를 발행한다.
* `onNext()` 이벤트를 전달하여 파란원 데이터를 발행한다.
* `onComplete()` 이벤트를 전달하여 데이터의 발행이 끝났음을 알린다.

### \#. Exam Code 
``` java
public static void main(String[] args) {
  // create() 함수를 이용하여 Observable을 생성한다.
  Observable<String> source = Observable.create(
    (ObservableEmitter<String> emitter) -> {
      emitter.onNext("red circle");
      emitter.onNext("blue circle");
      emitter.onComplete();
    }
  );

  // create() 함수로 생성된 Observable을 차가운 Observable이므로,
  // subscribe()을 호출하지 않으면, 데이터를 실제로 발행하지 않는다.
  source.subscribe(System.out::println);
}
```

[marble-diagram]: http://reactivex.io/documentation/ko/operators/images/create.c.png