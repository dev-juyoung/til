# node.js 설치하기 (공식문서를 이용한 방법)
> 해당 문서는 Ubuntu 16.04 LTS 버전을 기반으로 작성했으며, [공식사이트][docs-installation]를 참고하여 작성하였다.

`node.js`는 Chrome V8 JavaScript 엔진으로 빌드된 서버측 프레임워크이다.  
이벤트 기반 및 non-blocking i/o 모델을 사용해 가볍고 효율적이라고 한다.

Ubuntu 16.04 LTS에서 Node.js의 설치는 굉장히 간단하다.

``` bash
$ curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
$ sudo apt-get install -y nodejs
```

해당 문서를 정리하는 일자를 기준으로 8.x 버전이 LTS 버전이며, 가장 최신버전은 9.7.1 버전으로 확인된다.

만약, 최신버전인 9.x 버전을 사용하고 싶다면, `curl` 커맨드의 `setup_8.x` 부분을 `setup_9.x`로 변경하면 된다.


npm에서 네이티브 애드온을 컴파일하고 실행하려면, 빌드도구를 설치하여야 한다.  
선택사항이므로 생략하여도 큰 문제는 없다.

``` bash
$ sudo apt-get install -y build-essential
```

[docs-installation]: https://nodejs.org/ko/download/package-manager/