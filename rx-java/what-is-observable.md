# Observable이란

Observable 클래스는 데이터의 흐름에 맞게 알림을 전달하여 구독자가 데이터를 처리할 수 있도록 해주는 클래스이다.

RxJava의 Observable 클래스에는 세 가지의 알림을 구독자에게 전달 할 수 있다.

* onNext
  * 데이터의 발행을 알린다.
* onComplete
  * 모든 데이터의 발행이 완료 되었음을 알린다.
* onError
  * 특정 사유로 인해 Observable에서 에러가 발생했음을 알린다.
  * onError 이벤트 발생 이후에는 onNext 및 onComplete 이벤트가 발생하지 않는다.