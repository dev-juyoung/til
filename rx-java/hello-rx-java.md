# RxJava Hello World 출력해보기.

RxJava는 반응형 프로그래밍을 쉽게 할 수 있도록 제공되는 Library이다.  

Lambda를 몰라도 상관 없으나, 코드의 가독성 등을 위하여 Lambda에 대한 배경 지식이 있으면 더 좋다.

```java
public static void main(String[] args) {
  Observable.just("Hello", "World!")
  .subscribe(System.out::println);
}
```

* Observable
  * 데이터의 변화가 발생하는 데이터 소스.
* just()
  * Observable을 선언하는 가장 단순한 방법.
  * 실제 발행할 데이터를 지정한다.
* subscribe()
  * 데이터의 변화를 감시할 구독자 역할을 한다.
  * subscribe를 호출하지 않으면, 실직적인 데이터의 발행은 발생하지 않는다.