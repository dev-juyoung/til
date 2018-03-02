# Git-Flow 훑어보기.

`git`을 사용하고 있거나, 관심이 있는 사용자라면 `xxx-flow`라는 용어를 한번쯤은 들어봤을 것 같다.

정확한 의미를 해석하기는 힘들지만, 대략적으로 이해한 내용으로는,  
`git`의 `branch` 기능을 전략적으로 운용 및 관리하는데 목적이 있는 것 같다.

이러한 방법 중에는 `git-flow`, `github-flow`, `gitlab-flow` 등의 방법들이 제시되고 있다.

아래의 다이어그램 이미지는, 가정 대표적인 방법인 `git-flow`에 대한 다이어그램이다.

![git-flow][git-flow-diagram]

해당 다이어그램을 처음보는 사용자라면 조금은 복잡하게 느껴질 수 있겠지만,  
각 `branch`의 명칭과 용도를 이해한다면 조금 더 쉽게 느껴질 것이다.

* master
  * 최종적으로 릴리즈한 안정화 버전.
  * 언제든 production 가능한 상태의 결과물이 보관되어 있다.
* develop
  * 다음 릴리즈를 위한 개발중인 최신 버전.
  * master branch로부터 시작된다.
* feature
  * 특정 새로운 기능을 개발하기 위한 branch.
  * develop branch로부터 시작된다.
* release
  * 개발이 완료된 후, 릴리즈 이전 최종 점검을 위한 branch.
* hotfix
  * 크리티컬한 버그로 인해 긴급 bugfix를 위한 branch.

### \#. git-flow 설치.
> macOS를 쓰고 있으며, Git과 Homebrew가 설치되어 있다는 가정하에 진행한다.

``` bash
$ brew install git-flow-avh
```

### \#. 기존 Git Repository에 Git-Flow 적용하기.

기존에 `git`으로 관리되고 있던 저장소에 `git-flow`를 적용하기 위해서는 `git flow` 명령어를 이용하여 초기화를 진행하여야 한다.

``` bash
$ git flow init
```

해당 명령어를 사용하면, 각 프로세스에서 사용 될 `branch`의 명칭을 custom하게 지정할 수 있다. 만약 기본 설정을 그대로 사용하겠다면, `-d` 옵션을 이용하면 된다.

해당 명령어 실행 시, 기본적으로 생성된 `master` 브랜치 이 외에 `develop` 브랜치도 생성된다.

### \#. 신규 개발 시작하기.

다음 릴리즈에 포함될 새로운 기능을 개발할 때는, `feature` 브랜치를 이용하여 개발을 진행한다.

아래의 예제 코드에서는 이해의 편리성을 위해 `payment`라는 기능을 개발한다고 가정한다.

``` bash
$ git flow feature start payment
```

해당 명령어를 실행하면 내부적으로 다음과 같은 동작을 취한다.
* 현재 `develop` 브랜치를 기준으로 `feature/payment` 라는 브랜치가 생성된다.
* 생성된 `feature/payment` 브랜치로 이동한다.

해당 명령어 실행 이 후에는, 기존에 git 명령어로 작업하 듯 변경사항을 기록해 나가면 된다.

### \#. 신규 개발 완료.

진행 중이던 기능의 개발이 완료되면 `git flow` 명령을 이용하여 개발이 완료되었음을 명시하면 된다.

``` bash
$ git flow feature finish payment
```

해당 명령어를 실행하면 내부적으로 다음과 같은 동작을 취한다.
* `feature/payment` 브랜치를 `develop` 브랜치로 병합(merge) 한다.
* 병합이 완료된 후, `feature/payment` 브랜치는 삭제된다.

### \#. 프로덕션 모드로 릴리즈 하기 위한 점검 진행하기.

실제 사용자가 쓸 수 있도록 프로덕션에 배포하기 이전에, 내부적인 Q/A 등을 통해 버그를 찾아내고, 해당 버그들을 fix하는 작업을 진행한다.  
이때 사용되는 브랜치는 `release` 브랜치이다.

``` bash
$ git flow release start v0.0.1
```

해당 명령어를 실행하면 내부적으로 다음과 같은 동작을 취한다.
* 현재 `develop` 브랜치의 상태를 기준으로 `release/v0.0.1` 브랜치를 생성한다.
* 생성된 `release/v0.0.1` 브랜치로 이동한다.

해당 브랜치에서는 bugfix등의 작업이 진행되므로, 몇가지 사소한 commit이 발생할 수 있다.

또한, release의 명칭을 `vX.Y.Z` 형태로 버전명을 명시하듯 생성하였다.  
이는, 추후 해당 release를 완료할 때 `tag` 명칭으로 기록되므로, 새로 배포할 버전으로 기재하는 것이 좋을 것 같다.

### \#. 최종 점검 완료.

내부적인 Q/A 및 사소한 bugfix가 완료된 후, 최종적으로 프로덕션 모드에 배포할 준비가 완료된 상대라면, `git flow` 명령을 이용하여 점검이 완료되었음을 명시한다.

``` bash
$ git flow release finish v0.0.1
```

해당 명령어를 실행하면 내부적으로 다음과 같은 동작을 취한다.
* `release/v0.0.1` 브랜치를 `master` 브랜치로 병합(merge) 한다.
* 해당 `release`의 명칭으로 태그를 등록한다. `(v0.0.1)`
* `release/v0.0.1` 브랜치를 `develop` 브랜치로 재병합(back-merge) 한다.
* `release/v0.0.1` 브랜치를 삭제한다.

`feature` 및 `release`의 코드를 공유하기 위해 remote repository로 push/pull 할 수 있는 추가적인 명령어와 해당 자료에서 소개하지 않은 `hoxfix`와 관련된 명령어가 있으나, 해당 명령어들에 대해서는 공식 자료를 첨부하도록 하겠다.
> [Git-Flow CheatSheet 한국어 번역본][git-flow-document]

[git-flow-diagram]: http://nvie.com/img/git-model@2x.png
[git-flow-document]: https://danielkummer.github.io/git-flow-cheatsheet/index.ko_KR.html