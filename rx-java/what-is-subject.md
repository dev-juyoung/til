# Subject 클래스

`Subject` 클래스를 알기 이전에, Observable의 2가지 개념을 이해해야 된다.
* Cold Observable (차가운 Observable)
* Hot Observable (뜨거운 Observable)

`Cold Observable`은, Observable의 `just()`나 `fromIterable()`과 같은 함수를 호출하여도, `subscribe()` 함수를 호출하여 구독하지 않는 한, 데이터를 실질적으로 발행하지 않는다. 

반대로, `Hot Observable`은 `subscribe()` 함수,  
즉, 구독자의 존재 여부와 관계없이 실제로 데이터가 발행된다. 그렇기 때문에, `Hot Observable`의 경우, 구독자를 등록하여도 해당 Observable이 발행하는 데이터를 처음부터 끝까지 모두 수신할 수 있다는 보장이 없다.

다시 한번, 쉽게 정리를 하자면,
* Cold Observable
  * `subscribe()` 함수가 호출되어야만 준비된 데이터가 발행되기 시작함.
  * 구독자는 해당 Observable이 준비한 데이터를 처음부터 끝까지 전달 받음.
* Hot Observable
  * `subscribe()` 함수를 호출하지 않아도 준비된 데이터가 발행되기 시작함.
  * 구독자는 해당 Observable을 구독하기 시작한 시점부터 데이터를 전달 받음.
* ex) 1부터 10까지의 데이터가 준비되어 있는 Observable인 경우.
  * `Cold Observable`
    * 구독자(`subscribe()`)을 호출하면, 1부터 10까지 모든 데이터를 수신 받을 수 있다.
  * `Hot Observable`
    * 데이터가 발행 된 후, `5`의 시점에 구독자(`subscribe()`)을 호출하면, 5부터 10까지의 데이터만 수신 받을 수 있다. **(1 ~ 4는 못받음)**

`Cold Observable`의 예로는 `웹 요청`, `데이터베이스 쿼리` 등,  
보통 개발자의 의도에 따라 **특정 시점**에 **특정한 URL이나 데이터**를 지정하면 서버나 데이터베이스로 요청을 하고 결과를 받아오는 케이스가 있다.

`Hot Observable`의 예로는, `클릭 이벤트`, `키보드 이벤트`, `센서 데이터` 등과 같이,  
**불규칙한 시점**에 어떠한 액션 등으로 처리되고 결과를 전달하는 케이스가 있을 것 같다. 예를 들어 온도/습도 센서의 데이터를 처리하는 앱이라면 가장 최신의 온도와 습도 정보만 사용자에게 표시하면 되는 방식의 앱이 있을 것이다.

해당 자료의 주 쟁점인,   
`Subject` 클래스는 `Cold Observable`을 `Hot Observable`로 변환해주는 클래스이다.

특히, `Subject` 클래스는 Observable처럼 데이터를 발행 할 수도 있고, 구독자처럼 발행된 데이터를 처리할 수도 있다.  
즉, `Observable`의 속성과 `구독자`의 속성을 모두 가지고 있다는 것이 특징이다.

`Subject` 클래스에는 `AsyncSubject`, `BehaviorSubject`, `PublishSubject`, `ReplaySubject` 등이 있다.