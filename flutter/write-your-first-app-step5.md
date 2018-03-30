# Flutter Write Your First App.
> 해당 문서는 [공식 사이트][official-docs]의 `Write Your First App` 파트를 진행하며 정리하는 문서이다.

## Step.5
* [참고 Repository][tutorial-repository]

`Step.5`에서는 사용자의 인터렉션과 관련된 부분을 중점적으로 다룬다.

### \#. 상태 저장을 위한 변수 생성 및 인터렉션 가능한 UI 추가.

``` dart
class RandomWordsState extends State<RandomWords> {
  // ...other code
  final _saved = new Set<WordPair>();

  Widget _buildRow(WordPair pair) {
    final alreadySaved = _saved.contains(pair);

    return new ListTile(
      title: new Text(
        pair.asPascalCase,
        style: _biggerFont,
      ),
      trailing: new Icon(
        alreadySaved ? Icons.favorite : Icons.favorite_border,
        color: alreadySaved ? Colors.red : null,
      ),
    );
  }
  
  // ...other code
}
```

인터렉션 결과에 따른 상태 저장을 위한 `_save`라는 명칭을 가진 `private` 클래스 멤버변수가 하나 추가되었다.

또한, `_buildRow` 메서드 내부에 인터렉션 결과에 따른 아이콘 변경을 위한 `alreadySaved` 변수와, `ListTile`의 `trailing` 속성을 이용하여, 
해당 리스트 아이템 우측에 아이콘을 추가해주었다.

### \#. 인터렉션 처리

``` dart
class RandomWordsState extends State<RandomWords> {
  // ...other code

  Widget _buildRow(WordPair pair) {
    final alreadySaved = _saved.contains(pair);

    return new ListTile(
      // ...other code
      onTap: () {
        setState(() {
          if (alreadySaved) {
            _saved.remove(pair);
          } else {
            _saved.add(pair);
          }
        });
      },
    );
  }

  // ...other code
}
```

`ListTile`의 속성 중, `onTap` 속성을 이용하여 실질적인 인터렉션을 처리할 수 있다.  
해당 ListTile Widget에 `Tap Event`가 발생하면, `setState()` 메서드를 이용하여 상태를 변이시킬 수 있다.  
`setStae()` 메서드를 호출하여 상태를 변경하면, `State` 객체의 `build()` 메서드가 호출되며 UI가 업데이트 된다고 한다.

혹시라도 `React.js`를 경험해보았다면 `setState()` 메서드가 생소하지 않을 것으로 생각되는데,  
실질적으로 `Flutter`의 공식문서를 보면 `Flutter`는 React진영에서 많은 영감을 얻은 것으로 판단된다.

### \#. 실행 결과
> 좌측: Android Emulator / 우측: iOS Emulator

![Result Images][result-image]


[official-docs]: https://flutter.io/get-started/codelab/
[prev-post]: https://github.com/dev-juyoung/til/blob/master/flutter/write-your-first-app-step4.md
[tutorial-repository]: https://github.com/dev-juyoung/flutter-tutorials/tree/step-5

[result-image]: https://github.com/dev-juyoung/til-resources/blob/master/flutter/write-your-first-app/step-5-interactivity.png