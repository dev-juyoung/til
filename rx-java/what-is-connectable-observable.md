# ConnectableObservable 클래스

`ConnectableObservable` 클래스는 Subject 클래스처럼 Cold Observable을 Hot Observable로 변환하며, Observable을 여러 구독자에게 공유할 수 있으므로 원 데이터 하나를 여러 구독자에게 동시에 전달할 때 사용한다.

`ConnectableObservable` 객체를 생성하기 위해서는 먼저 Observable에 `publish()` 함수를 호출해 주어야 하며, 이 `publish()` 함수는 여러 구독자에게 데이터를 발행하기 위해 `connect()` 함수를 호출하기 전까지 데이터의 발행을 유에시키는 역할을 한다.

### \#. Marble Diagram
![Marble Diagram][marble-diagram]

* Observable을 통해 발행할 **원 데이터**는 `빨간원`, `녹색원`, `파란원` 이다.
* 해당 Observable에 `publish()` 함수를 호출하여 `ConnectableObservable객체`를 생성한다.
* `connect()` 함수 호출 이전에, `첫번째 구독자`와 `두번째 구독자`가 구독을 시작한다.
* `connect()` 함수를 통해 실제 데이터를 발행하기 시작한다.
* `connect()` 함수 호출 이 후, `세번째 구독자`가 구독을 시작한다.
* 모든 데이터의 발행을 완료한다.

조금은, 난해한 해석일 수 있으나 아래의 코드와 함께 분석하면 쉽게 이해할 수 있을 것으로 보인다.

### \#. Exam Code
``` java
public static void main(String[] args) {
  String[] dataSet = { "red ball", "green ball", "blue ball" };

  Observable<String> observable = 
    Observable.interval(100L, TimeUnit.MILLISECONDS)
      .map(Long::intValue)
      .map(i -> dataSet[i])
      .take(dataSet.length);

  ConnectableObservable<String> source = observable.publish();
  source.subscribe(data -> System.out.println("첫번째 구독자 => " + data));
  source.subscribe(data -> System.out.println("두번째 구독자 => " + data));
  source.connect();

  sleep(250)
  source.subscribe(data -> System.out.println("세번째 구독자 => " + data));
  sleep(100)
}

// Thread sleep을 위한 method.
public static void sleep(int millis) {
  try {
    Thread.sleep(millis);
  } catch (InterruptedException e) {
    e.printStackTrace();
  }
}
```

[marble-diagram]: http://reactivex.io/documentation/operators/connect.html
