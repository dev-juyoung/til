# ReplaySubject 클래스

`ReplaySubject` 클래스는 `Subject` 클래스 중, 가장 특이하며 사용할 때 주의해야 되는 클래스이다.  
`Subject` 클래스의 목적은 Hot Observable을 활용하는 것인데, 마치 Cold Observable을 사용하듯 동작하기 때문이다.

클래스의 이름에서 예상 할 수 있듯이, `ReplaySubject` 클래스는 구독자의 구독 시점과 상관없이 항상 데이터의 처음부터 끝까지 발행하는 것을 보장해준다.

그러므로, 모든 데이터 내용을 저장해두는 과정 중 메모리 누수가 발생할 가능성을 염두에 두고 사용할 때 주의하여야 한다.

### \#. Marble Diagram
![Marble Diagram][marble-diagram]

해당 마블다이어그램을 해석하면 다음과 같을 것으로 보인다.

* ReplaySubject를 생성한 후, `첫번째 구독자`가 구독을 시작한다.
* `빨간원`과 `녹색원`의 데이터를 발행한 후, `두번째 구독자`가 구독을 시작한다.
* 마지막으로 `파란원` 데이터를 발행 한 후 데이터의 발행을 완료한다.

### \#. Exam Code
``` java
public static void main(String[] args) {
  ReplaySubject<String> subject = ReplaySubject.create();
  subject.subscribe(data -> System.out.println("첫번째 구독자 => " + data));
  subject.onNext("red ball");
  subject.onNext("green ball");
  subject.subscribe(data -> System.out.println("두번째 구독자 => " + data));
  subject.onNext("blue ball");
  subject.onComplete();
}
```

해당 예제 코드를 실행해보면,  
다른 Subject 클래스와는 다르게, `두번째 구독자`가 구독을 시작하면 이전에 발행된 `red ball`과 `green ball` 데이터도 함께 전달 받을 수 있다는 것을 확인 할 수 있다.

[marble-diagram]: http://reactivex.io/documentation/operators/images/S.ReplaySubject.png