# Flutter 설치
> 해당 문서는 macOS High Sierra 10.13.3 버전을 기반으로 작성했으며, [공식사이트][official-docs]를 참고하여 작성하였다.

최근들어, 하나의 언어를 이용하여 Android 및 iOS를 지원할 수 있는 멀티플랫폼 언어가 핫해지고 있다.

멀티플랫폼 언어에는 최근들어 많이 핫해진, `NativeScript`와 `React Native`, `NativeScript-Vue` 등이 있을 것 같다.

하나의 언어를 가지고 두개의 플랫폼을 대응할 수 있다는 것은 충분히 매력이 있지만, 현재까지는 큰 관심을 가지고 있지 않았으나, **Google**이 `Flutter`라는 언어를 선보이녀 멀티플랫폼 언어의 영역을 개척하는 것을 확인하고 관심을 가져볼 필요성을 느끼게 되어 조금 살펴보고자 한다.

### \#. 필수 준비물
* git
* homebrew
* android studio 3.x

### \#. Flutter 설치 및 환경변수 저장.
* `git clone` 명령을 통해, `Flutter`를 내려 받는다.

``` bash
$ git clone -b beta https://github.com/flutter/flutter.git
$ export PATH=`pwd`/flutter/bin:$PATH
```
> 환경변수에 영구적으로 저장을 위해서는 본인의 설정에 맞는 환경설정 파일에 PATH를 잡아 주면 된다.

### \#. Flutter 종속성 확인.
* `flutter doctor` 명령어를 통해, 추가적으로 설치가 필요한 종속성이 있는지 확인한다.
* 해당 명령 실행 후, 커맨드의 출력문 중, **굵은 글씨**를 자세히 살펴보면 어렵지 않게 필요한 족속성 모듈을 설치할 수 있다.

``` bash
$ flutter doctor
```
> 해당 명령 실행 후, 출력되는 커맨드 라인을 확인 한 후, **굵은 글씨**와 추가적인 안내 문구를 확인하면 어렵지 않게 족속성 모듈을 설치할 수 있다.

### \#. IDE Setup.
> 개인적으로 안드로이드 개발자이므로, `Android Studio 3.0 이상` 설치되어 있다는 가정하에 진행한다.

* Android Studio를 실행한다.
* `Preferences > Plugins` 메뉴로 접근 한 후, `Browse repositories…`를 선택한다.
* `Flutter`를 검색 한 후, 설치를 진행하고 Android Studio를 재 실행 한다.
  > 플러그인 설치 시, `Dart plugin` 설치에 대한 팝업창이 뜰 경우, `Yes`를 눌러 함께 설치를 진행하여야 함.

[official-docs]: https://flutter.io/setup-macos/