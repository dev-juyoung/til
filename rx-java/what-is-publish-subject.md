# PublishSubject 클래스

`PublishSubject` 클래스는 `Subject` 클래스 중 가장 **일반적인** 클래스이다.  
구독자가 `subscribe()` 함수를 호출하면 값을 발행하기 시작한다.

`AsyncSubject` 클래스 처럼 마지막 값만 발행하거나, `BehaviorSubject` 클래스처럼 발행할 값이 없을 경우 기본 값을 제공하거나 하지 않는다.

### \#. Marble Diagram
![Marble Diagram][marble-diagram]

* PublishSubject를 생성한 후, `첫번째 구독자`가 구독을 시작한다.
* 이 후, `빨간원`과 `녹색원`의 데이터를 발행한 후, `두번째 구독자`가 구독을 시작한다.
* 마지막으로 `파란원` 데이터를 발행 한 후 데이터의 발행을 완료한다.

### \#. Exam Code
``` java
public static void main(String[] args) {
  PublishSubject<String> subject = PublishSubject.create();
  subject.subscribe(data -> System.out.println("첫번째 구독자 => " + data));
  subject.onNext("red ball");
  subject.onNext("green ball");
  subject.subscribe(data -> System.out.println("두번째 구독자 => " + data));
  subject.onNext("blue ball");
  subject.onComplete();
}
```

기본값을 제공하지 않기 때문에, `AsyncSubject`와 동일하게 `create()` 함수를 이용하여 Subject 클래스를 생성한다.


[marble-diagram]: http://reactivex.io/documentation/operators/images/S.PublishSubject.png
