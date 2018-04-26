# Go 설치
> 해당 문서는 macOS High Sierra 10.13.4 버전을 기반으로 작성하였다.

### \#. `PKG` 다운로드 및 설치
[공식사이트][download-url]로 접속하여, `pkg`파일을 내려받은 후 설치한다.

### \#. 설치 확인
`pkg` 프로그램을 이용하여 설치가 완료된 후, 제대로 설치 되었는지 확인이 필요하다.


다음의 명령어를 이용하여, 아래와 같은 결과 화면이 나온다면 정상적으로 설치된 것이다.

``` bash
$ ls -l /usr/local/go
```
![결과 화면][verify-image]

### \#. 환경변수 설정
터미널에서 `go` 명령어를 실행하기 위해서는 추가적으로 환경변수를 설정하여야 한다.

각자의 환경에 맞는 환경 설정 파일에 다음과 같은 문장을 추가하여주면 된다.
> 현재 `zsh`를 쓰고 있으므로 `.zshrc` 파일에 적용하였다.

``` bash
# ~/.zshrc
export PATH=$PATH:/usr/local/go/bin

# 이 후, 해당 환경설정 파일을 적용하기 위한 명령
$ source ~/.zshrc
```

설정을 완료한 후, 터미널에 `go` 또는 `go env`와 같은 명령어를 실행한 후, 제대로 출력이 된다면 설정이 잘 된 것으로 판단하여도 좋다.

### \#. Hello, World 출력해보기
다음의 코드를 가지는 `hello.go` 파일을 만든 후, `Hello, World`를 출력해보자.
``` go
package main
import "fmt"

func main() {
  fmt.Printf("Hello, World")
}
```
작성을 완료하였다면, `go` 명령어를 통해 실행해보자.
``` bash
$ go hello.go
> Hello, World
```


[download-url]: https://golang.org/dl/
[verify-image]: https://github.com/dev-juyoung/til-resources/blob/master/go/installation/verify-installation.png