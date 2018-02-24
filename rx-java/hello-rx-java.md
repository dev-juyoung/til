# RxJava2 훑어보기

RxJava는 2013년 넷플릭스의 기술 블로그를 통해 처음 소개되었다.  
`.NET` 환경에서의 리액티브 확장 라이브러리를 JVM에 포팅하여 만들어졌다.  

RxJava는 비동기 프로그래밍, 즉 `반응형 프로그래밍`을 쉽게 접근 할 수 있도록 제공된 라이브러리이다.

RxJava 학습에 있어, `Lambda`, `Stream API` 등 Java8에서 지원하는 기능을 몰라도 상관은 없으나, 코드의 가독성 등을 위하여 배경 지식을 가지고 있으면 더 좋은 개발 환경을 경험할 수 있다고 한다.

아래는 가장 기본적인 RxJava2의 샘플 코드이다.
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