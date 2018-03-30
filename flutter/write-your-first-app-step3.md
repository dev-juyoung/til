# Flutter Write Your First App.
> 해당 문서는 [공식 사이트][official-docs]의 `Write Your First App` 파트를 진행하며 정리하는 문서이다.

## Step.3
* [참고 Repository][tutorial-repository]

`Step.3`에서는 상태 기반 위젯에 대한 내용을 중점적으로 다룬다.

### \#. 상태 기반 위젯.

[이전에 작성된 TIL][prev-post]의 코드를 확인하여 보면, 작성된 `MyApp` 클래스는 머티리얼 라이브러리의 `StatelessWidget`을 상속받아 구현되었다.

단어의 뜻 그대로, `StatelessWidget`은 상태가 없는(?) 위젯이므로, 동적으로 특정 속성을 변경할 수 없다. 즉, Java언어로 비교를 해보았을 때, `StatelessWidget`를 상속받는 클래스는 모든 값들이 `final` 이라는 것이다.

그렇다면, `상태 기반 위젯`이란 반대로 상태를 저장하고 변경할 수 있는 위젯을 의미한다.

이러한 `상태 기반 위젯`을 구현하기 위해서는 최소 2가지의 클래스가 필요하다.
* State 클래스.
* State 클래스 인스턴스를 생성하는 StatefulWidget 클래스.


### \#. StatefulWidget 클래스 구현.

해당 Widget만을 위한 `.dart` 파일을 따로 분리할 수 있지만, 튜토리얼에 그치는 예제이므로 기존에 작성 중이던 `main.dart` 파일에 이어서 작성하겠다.

해당 `main.dart` 파일 어디에 위치시켜도 상관 없으나, 해당 파일의 **최하단**에 이어 작성하면 된다.


``` dart
class RandomWords extends StatefulWidget {
  @override
  createState() => new RandomWordsState();
}
```

위에서 `상태 기반 위젯`을 작성하기 위해서는 최소 2개의 클래스가 필요하다고 하였는데, 여기서 그 이유를 알 수 있다.

`StatefulWidget`클래스 자체는 상태를 변경할 수 없다.  
그렇기에 `State`를 상속받아 구현하는 추가적인 클래스가 필요하다.

이러한 구조적인 특성을 보여주듯,  
머티리얼 라이브러리의 `StatefulWidget` 클래스를 상속받게 되면, 필수적으로 `createState()` 메서드를 구현해주어야 하며, 해당 메서드는 상태 관리를 위한 `State` 클래스 인스턴스를 생성한다.

현재까지는 아직 `State` 클래스를 구현하지 않았기에 컴파일 에러가 발생하겠지만, 무시하여도 좋다.

### \#. State 클래스 구현.

``` dart
class RandomWordsState extends State<RandomWords> {
  @override
  Widget build(BuildContext context) {
    final wordPair = new WordPair.random();
    return new Text(wordPair.asPascalCase);
  }
}
```

`State` 클래스에는 실질적인 상태정보와 해당 Widget이 어떠한 방식으로 표출될지에 대한 구현내용 대부분이 담겨져 있다.

해당 `RandomWordsState`클래스는 임의이 단어를 생성하고, `TextView`로 표출할 수 있도록 Widget을 생성하여 반환한다.

### \#. 상태 기반 위젯 반영.

`상태 기반 위젯`을 생성하였으니, 이를 `MyApp` 클래스에 반영한다.

``` dart
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
          child: new RandomWords(),
        ),
      ),
    );
  }
}
```

`RandomWordsState` 클래스에서 임의의 영단어를 생성한 후 `Text Widget`을 반환하도록 하였으며, 해당 `State` 클래스 인스턴스를 `RandomWords`에서 가지고 있도록 `상태 기반 위젯`을 만들어 주었으므로, `MyApp` 클래스에서는 불필요한 임의의 영단어 생성 코드를 제거하고, 우리가 생성한 `RandomWords` 클래스의 인스턴스를 이용하여 화면에 표출하도록 변경하였다.

[기존코드][prev-post]와 비교하여 본다면 조금 더 명확하게 구분이 갈 것이라 판단된다.

[이전 TIL의 결과화면][prev-post]과 결과화면의 차이는 없으므로, 이번 `Step.3`에서는 결과화면을 첨부하지 않도록 하겠다.
~~사실 귀찮음...~~

[official-docs]: https://flutter.io/get-started/codelab/
[prev-post]: https://github.com/dev-juyoung/til/blob/master/flutter/write-your-first-app-step2.md
[tutorial-repository]: https://github.com/dev-juyoung/flutter-tutorials/tree/step-3