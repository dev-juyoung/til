# Flutter Write Your First App.
> 해당 문서는 [공식 사이트][official-docs]의 `Write Your First App` 파트를 진행하며 정리하는 문서이다.

## Step.4
* [참고 Repository][tutorial-repository]

`Step.4`에서는 기존에 작성한 StatefulWidget 코드를 변경하여, 무한 스크롤이 가능한 ListView를 생성하는 방법에 대하여 중점적으로 다룬다.

### \#. 상태 저장을 위한 변수 생성.

``` dart
class RandomWordsState extends State<RandomWords> {
  // WordPair 타입의 배열 변수.
  final _suggestions = <WordPair>[];
  // 텍스트의 크기를 설정하기 위한 변수.
  final _biggerFont = const TextStyle(fontSize: 18.0);

  // ...other code
}
```

`Dart` 언어에서 변수 또는 메서드명 앞에 `언더바(_)`가 붙을 경우,
`private` 접근제한자가 된다.

실제 프로그램 작성 시, 외부에서 접근을 할 수 없도록 할 때 유용하므로 외워두면 좋을 듯하다.

### \#. ListView 생성

``` dart
class RandomWordsState extends State<RandomWords> {
  // ...other code

  Widget _buildRow(WordPair pair) {
    return new ListTile(
      title: new Text(
        pair.asPascalCase,
        style: _biggerFont,
      ),
    );
  }

  Widget _buildSuggestions() {
    return new ListView.builder(
        padding: const EdgeInsets.all(16.0),
        itemBuilder: (context, i) {
          if (i.isOdd) return new Divider();

          final index = i ~/ 2;

          if (index >= _suggestions.length) {
            _suggestions.addAll(generateWordPairs().take(10));
          }
          return _buildRow(_suggestions[index]);
        }
    );
  }

  // ...other code
}
```

위의 코드에서 2가지의 `private` 메서드가 추가되었음을 확인 할 수 있다.

`_buildRow` 메서드의 경우 `WordPair`를 전달받아, `Text Widget`을 생성하고 해당 `WordPair`를 표출하는 역할을 한다.

`_buildSuggestions` 메서드에서는 실질적인 특정 조건을 판단하여 `데이터(state)`의 갱신과 ListView Widget을 생성하여 반환하고 있다.

`Flutter`에서의 ListView는 `Builder Pattern`을 이용하여 객체를 생성하는 방법을 채택한 것으로 보이며, 이를 위해 `builder()` 메서드를 제공하고 있는것으로 확인된다. ~~Builder Pattern이 아닐수도...~~

해당 `builder()` 메서드에서는 몇가지 ListView의 표출을 위한 속성을 지정할 수 있는 것으로 보이며, 특히 `itemBuilder`라는 필수 속성을 필요로한다.

`itemBuilder` 속성은 `BuilderContext`와 `index` 값을 전달받는 익명의 콜백함수를 구현하면 된다.

`Android`의 `RecyclerView`나, `iOS`의 `CollectionView`와 비교한다면, 
`RecyclerView.Adapter`나 `UICollectionViewDataSource.collectionView(_:cellForItemAt:)` 와 비슷한 역할이지 않을까라는 생각이 든다.

### \#. ListView 적용.

``` dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Welcome to Flutter',
      home: new RandomWords(),
    );
  }
}

class RandomWordsState extends State<RandomWords> {
  // ...other code

  @override
  Widget build(BuildContext context) {
    return new Scaffold (
      appBar: new AppBar(
        title: new Text('Startup Name Generator'),
      ),
      body: _buildSuggestions(),
    );
  }
}
```
`RandomWordsState`에서 Scaffold와 AppBar등이 관리될 것이므로, 기존의 `MyApp`에서 생성하였던 `Scaffold` 객체를 제거하고, `RandomWords` 클래스 인스턴스를 생성하여 `home`으로 지정한다.

### \#. 실행 결과
> 좌측: Android Emulator / 우측: iOS Emulator

![Hello World][result-image]


[official-docs]: https://flutter.io/get-started/codelab/
[prev-post]: https://github.com/dev-juyoung/til/blob/master/flutter/write-your-first-app-step3.md
[tutorial-repository]: https://github.com/dev-juyoung/flutter-tutorials/tree/step-4

[result-image]: https://github.com/dev-juyoung/til-resources/blob/master/write-your-first-app/step-4-listview.png