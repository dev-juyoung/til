# just() 함수

RxJava2의 Observable을 생성하는 함수 중, 가장 간단한 방법 중 하나이다.

`just()` 함수로 전달 된 매개변수 값을 발행하기 위해 Observable을 생성하며, 최대 10개까지의 데이터를 발행할 수 있도록 준비되어 있다.

단, 주의할 점은 `just()` 함수로 전달하는 매개변수의 타입이 모두 동일한 데이터 타입이여야 한다.

### \#. Marble Diagram
---
![Marble Diagram][marble-diagram]

* 빨간원 데이터를 `just` 함수에 전달하면, 전달된 데이터 그대로 빨간원 데이터가 발행된다.
* 하단의 `파이프(|)`는 데이터의 발행이 끝남을 구독자에게 알린다. `onComplete()`

### \#. Exam Code 
``` java
public static void main(String[] args) {
  Observable
  .just("red circle")
  .subscribe(System.out::println);
}
```

[marble-diagram]: http://reactivex.io/documentation/operators/images/just.c.png