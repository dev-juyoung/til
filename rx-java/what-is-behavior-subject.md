# BehaviorSubject 클래스

`BehaviorSubject` 클래스는 구독자가 구독을 시작하면, 가장 최근 값 또는 기본 값을 전달해 주는 `Subject` 클래스이다.  
얼핏보면 `AsyncSubject`와 비슷한게 아닌가? 라는 의문을 품을 수 있지만 실제 동작을 보면 완전히 다르게 동작함을 알 수 있다.

[AsyncSubject][prev-post]는 `onComplete()` 이벤트가 전달되기 직전의 `onNext()` 이벤트에만 관심을 가지며, 그 이전의 `onNext()` 이벤트로 전달되는 데이터는 모두 무시된다.

허나, `BehaviorSubject`는 구독자가 구독을 시작한 시점을 기점으로, 가장 최근에 발행된 데이터 또는 발행된 데이터가 없을 경우 기본 값을 전달하며, `onComplete()` 이벤트가 발생하기 이전까지 지속적으로 데이터를 전달한다.

마블다이어그램을 확인하면 조금 더 이해가 쉬울 수 있다.

### \#. Marble Diagram
![Marble Diagram][marble-diagram]

해당 마블다이어그램을 해석하면 다음과 같이 해석할 수 있을 것 같다.

* BehaviorSubject를 생성할 때, `분홍원`을 기본값으로 가지도록 생성한다.
* 데이터를 발행하기 이전에 `첫번째 구독자`가 구독을 시작하며, 해당 구독자는 기본 값인 `분홍원`을 전달 받는다.
* 이 후, `빨간원`과 `녹색원` 데이터를 발행하고, `두번째 구독자`가 구독을 시작하며, 해당 구독자는 구독 직전에 발행된 마지막 데이터인 `녹색원`을 전달 받는다.
* 마지막으로 `파란원` 데이터를 발행 한 후, 데이터의 발행을 완료한다.

### \#. Exam Code
``` java
public static void main(String[] args) {
  BehaviorSubject<String> subject = BehaviorSubject.createDefault("pink ball");
  subject.subscribe(data -> System.out.println("첫번째 구독자 => " + data));
  subject.onNext("red ball");
  subject.onNext("green ball");
  subject.subscribe(data -> System.out.println("두번째 구독자 => " + data));
  subject.onNext("blue ball");
  subject.onComplate();
}
```

해당 코드를 확인해보면, [AsyncSubject][prev-post]와는 다르게, `createDefault()` 함수를 이용하여 Subject를 생성한다.

이는, `BehaviorSubject`의 경우, 데이터가 없는 경우라도 **기본 값**을 전달할 수 있어야 하므로 `create()`가 아닌 `createDefault()` 함수를 이용하여 Subject를 생성하는 것이다.

[marble-diagram]: http://reactivex.io/documentation/operators/images/S.BehaviorSubject.png
[prev-post]: https://github.com/dev-juyoung/til/blob/master/rx-java/what-is-async-subject.md