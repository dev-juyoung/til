# Flutter Write Your First App.
> 해당 문서는 [공식 사이트][official-docs]의 `Write Your First App` 파트를 진행하며 정리하는 문서이다.

## Step.1
* [참고 Repository][tutorial-repository]

### \#. 필수 준비물.
* Flutter
* Android Studio 3.0 higher

Flutter 개발환경이 설치되어 있지 않다면, [이전에 작성한 TIL][prev-post]을 확인하여 선 진행되어야 한다.

### \#. 프로젝트 생성.
* Android Studio 의 `File > New > New Flutter Project...` 메뉴를 이용하여 적절한 입력값과 Path를 지정하여 새로운 `Flutter Project`를 생성한다.

### \#. Flutter 세계의 빠져보자.
모든 프로그래밍 언어를 학습할 때, 가장 시작하기 쉬운 방법은 첫번째 프로그램으로 간단한 `Hello World`를 출력하는 것이다.

``` dart
import 'package:flutter/material.dart';

void main() => runApp(new MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Welcome to Flutter',
      home: new Scaffold(
        appBar: new AppBar(
          title: new Text('Welcome to Flutter'),
        ),
        body: new Center(
          child: new Text('Hello World'),
        ),
      ),
    );
  }
}
```

공백을 포함하여 20줄이면 `Hello World`를 화면에 출력하는 Application을 간단하게 만들어버릴 수 있다.

### \#. Hello world 코드 뜯어보기.
* `import 'package:flutter/material.dart';`
  * Google의 공식적인 디자인 가이드인 [머티리얼 디자인][material-guide]이 적용된 Application을 만들기 위한 의존성 추가.

* `void main() => runApp(new MyApp());`
  * 해당 프로그램의 진입점.
  * Dart 언어에서는 한 줄 짜리의 함수 또는 메서드를 `=>` 키워드를 이용하여 축약된 표현식을 사용할 수 있다.
  * Javascript의 Arrow Function과 비슷한 형태이나, Javascript와는 다른 용도로 사용된다.

* `MyApp class`
  * Flutter는 모든 것이 `Widget`으로 구성된다고 한다.
  * 위에서 import한 `material.dart`에서 제공되는 `StatelessWidget` 클래스를 상속받고, 해당 `MyApp` 클래스가 어떠한 구조의 UI를 표출할 지 정의되어 있다.

### \#. 실행 결과
> 좌측: Android Emulator / 우측: iOS Emulator

![Hello World][result-image]


[official-docs]: https://flutter.io/get-started/codelab/
[prev-post]: https://github.com/dev-juyoung/til/blob/master/flutter/installation-flutter.md
[material-guide]: https://material.io/guidelines/
[tutorial-repository]: https://github.com/dev-juyoung/flutter-tutorials/tree/step-1

[result-image]: https://github.com/dev-juyoung/til-resources/blob/master/write-your-first-app/step-1-helloworld.png