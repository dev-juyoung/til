# AsyncSubject 클래스

`AsyncSubject` 클래스는 Observable에서 발행한 **마지막 데이터**를 얻어 올 수 있는 `Subject`클래스이다.

완료되기 전 마지막 데이터에만 관심이 있고, 그 외의 데이터는 무시된다.
즉, `onComplete()` 이벤트가 전달되기 직전의 `onNext()` 이벤트에만 관심을 가진다는 뜻으로 해석하면 될 듯 하다.

아래의 마블다이어그램을 보면 이해되겠지만, 기본적인 Operator를 이용한 Observable과는 다르게, 여러개의 구독자(`subscribe()`)를 가질 수 있다.

### \#. Marble Diagram

![Marble Diagram][marble-diagram]

해당 마블다이어그램을 해석하면 다음과 같을 것으로 보인다.

* 데이터를 발행하기 이전에 `첫번째 구독자`가 구독을 시작한다.
* 이 후, `빨간원` 과 `녹색원` 데이터를 발행하고, `두번째 구독자`가 구독을 시작한다.
* 마지막으로, `파란원` 데이터를 발행 한 후, 데이터의 발행을 완료한다.


### \#. Exam Code

``` java
public static void main(String[] args) {
  AsyncSubject<String> subject = AsyncSubject.create();
  subject.subscribe(data -> System.out.println("첫번째 구독자 =>" + data));
  subject.onNext("red circle");
  subject.onNext("green circle");
  subject.subscribe(data -> System.out.println("두번째 구독자 => " + data));
  subject.onNext("blue circle");
  subject.onComplete();
}
```

### \#. 구독자로 동작하는 AsyncSubject 클래스
[Subject 클래스][prev-docs]에 대한 문서를 보면, Subject 클래스의 특징 중 `Observable의 속성`과 `구독자의 속성`을 모두 가지고 있다고 정리하였다.

위의 예제코드가 `Observable의 속성`을 가진 Subject이다.

그렇다면, `구독자의 속성`을 가지는 Subject의 코드는 어떻게 작성하는지 알아보자.

``` java
public static void main(String[] args) {
  // 발행할 데이터
  Float[] temperature = { 10.1f, 13.4f, 12.5f };
  // fromArray() 함수를 이용한 Observable을 생성한다.
  Observable<Float> source = Observable.fromArray(temperature);
  // 구독자로 동작할 AsyncSubject 클래스를 생성한다.
  AsyncSubject<Float> subject = AsyncSubject.create();
  subject.subscribe(data -> System.out.println("현재 온도는 [" + data + "] 입니다."));
  // Observable의 구독자로 AsyncSubject를 등록한다.
  source.subscribe(subject);
}
```

이렇게, `Subject 클래스`가 `Observable의 속성`과 `구독자의 속성`을 모두 가질 수 있는 이유는 `Subject` 클래스가 `Observable`을 상속하고 있으며, 동시에 `Observer Interface`를 구현하였기 떄문이다.

[marble-diagram]: http://reactivex.io/documentation/operators/images/S.AsyncSubject.png
[prev-docs]: https://github.com/dev-juyoung/til/blob/master/rx-java/what-is-subject.md




