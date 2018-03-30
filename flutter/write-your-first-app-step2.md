# Flutter Write Your First App.
> 해당 문서는 [공식 사이트][official-docs]의 `Write Your First App` 파트를 진행하며 정리하는 문서이다.

## Step.2
* [참고 Repository][tutorial-repository]

`Step.2` 에서는 외부 라이브러리를 추가하는 방법과 적용하는 방법에 대하여 중점적으로 다룬다.

해당 튜토리얼에서는 `english_words` 라이브러리만 사용한다.  
실제 개발 시 필요한 라이브러리가 있는지 궁금하다면 [Flutter Packages][search-modules] 사이트를 방문하여 확인해보면 된다.

### \#. 외부 라이브러리 추가.
Flutter는 `pubspecs.yaml` 파일을 통해 해당 프로젝트의 전반적인 환경을 설정할 수 있다.

``` yaml
dependencies:
  flutter:
    sdk: flutter

  cupertino_icons: ^0.1.0
  english_words: ^3.1.0
```
`pubspecs.yaml` 파일을 연 후, `dependencies` 블럭에 원하는 라이브러리를 `라이브러리명: 버저닝`을 명시해주면 된다.

이 후, `Android Studio` 기준으로 우측 상단에 표시되는 `Pacakges get` 버튼을 클릭하면 프로젝트에 해당 모듈을 다운로드 받은 후, 동기화 작업을 진행한다.

프로젝트로 포함된 라이브러리는 `External Libraries > Dart Packages`에서 해당 라이브러리 명칭의 directory로 확인 가능하다.

추가적으로 `dependencies` 블럭 하단에 `dev_dependencies` 블럭이 따로 존재하는 것으로 보았을 때, 개발 시에만 필요한 dependencies는 `dev_dependencies` 포함하여 작업하면 될 것으로 보인다.

### \#. 외부 라이브러리 사용.
[이전에 작성한 TIL][prev-post]에서 작성한 Hello World 프로그램의 제일 상단에 사용하였던 `import` 문을 통해 외부 라이브러리를 사용할 수 있다.

``` dart
import 'package:flutter/material.dart';
// english_words 라이브러리를 사용하기 위해 명시.
import 'package:english_words/english_words.dart';

void main() => runApp(new MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // english_words의 WordPair 클래스를 이용하여 무작위 단어를 생성한다.
    final wordPair = new WordPair.random();
    return new MaterialApp(
      title: 'Welcome to Flutter',
      home: new Scaffold(
        appBar: new AppBar(
          title: new Text('Welcome to Flutter'),
        ),
        body: new Center(
          // 생성된 단어를 화면에 Text View로 표출한다.
          child: new Text(wordPair.asPascalCase),
        ),
      ),
    );
  }
}
```

기존 코드를 계속 활용할 것이므로, 주석이 처리된 부분을 중점으로 확인하면 된다.

### \#. 실행 결과
> 좌측: Android Emulator / 우측: iOS Emulator

![Hello World][result-image]


[official-docs]: https://flutter.io/get-started/codelab/
[search-modules]: https://pub.dartlang.org/flutter/
[prev-post]: https://github.com/dev-juyoung/til/blob/master/flutter/write-your-first-app-step1.md
[tutorial-repository]: https://github.com/dev-juyoung/flutter-tutorials/tree/step-2

[result-image]: https://github.com/dev-juyoung/til-resources/blob/master/write-your-first-app/step-2-external-lib.png