# node.js 설치하기 (nvm을 이용한 방법)

[공식 문서에서 안내하는 Node.js 설치][prev-post]방법은, 하나의 컴퓨터에서 하나의 Node.js 버전만 사용할 수 있다.

하지만, 프로젝트를 동시에 여러개 진행하다보면, 프로젝트마다 버전이 틀려지는 경우도 발생하기 마련이다.

이러한 상황에서 `nvm`을 이용하면 좋다.  
`nvm`은 간편하게 하나의 컴퓨터에서 다양한 Node.js 버전을 설치하고 관리할 수 있도록 해주는 Node.js 만의 `패키지 관리 Tool`이라고 보면 편할 것 같다.

### \#. nvm 설치

계정의 루트 디렉토리에서, `curl` 또는 `wget` 명령어를 통해 설치할 수 있다.

``` bash
$ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash
```

해당 명령어를 실행하면 다음과 같은 작업이 진행된다.
* `nvm repository`를 `.nvm` 으로 복제한다.
* `.bash_profile`, `.zshrc`, `.profile`, `.bashrc` 등, 자신의 환경에 맞는 환경설정 파일에 NVM과 관련된 필요한 코드를 작성한다.
  ``` bash
  export NVM_DIR="$HOME/.nvm"
  [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
  ```

환경설정 코드가 작성이 되었다 하더라도, 바로 적용은 되지 않는다.  
커맨드를 재 실행하거나, `source {filePath}` 명령어를 이용하여 환경설정 파일을 리로드 해주는 방법이 있다.

### \#. node.js lts 버전 설치하기.

`nvm` 설치가 완료되었다면, 다음 명령어를 실행하여 간편하게 Node.js LST 버전을 설치할 수 있다.

``` bash
$ nvm install --lts
```

해당 문서는 `nvm`을 이용한 Node.js의 설치를 다루기 위한 문서이므로,  
`nvm 명령어`에 대해서는 [공식 Github][nvm-github]를 확인하기 바란다.

[nvm-github]: https://github.com/creationix/nvm