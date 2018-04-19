# Ubuntu의 apt-get 명령어

`apt-get`은 ubuntu를 포함한 데비안 계열의 리눅스에서 쓰이는 패키지 관리 명령어 도구이다.

* 패키지 인덱스 정보 업데이트
  ``` bash
  $ sudo apt-get update
  ```
* 설치된 패키지 업그레이드
  ``` bash
  $ sudo apt-get upgrade
  ```
* 설치된 패키지 의존성 검사하며 업그레이드
  ``` bash
  $ sudo apt-get dist-update
  ```
* 패키지 설치
  ``` bash
  $ sudo apt-get install {packageName}
  ```
* 패키지 의존성 검사하며 설치
  ``` bash
  $ sudo apt-get dist-install {packageName}
  ```
* 패키지 삭제
  ``` bash
  $ sudo apt-get remove {packageName}
  ```
* 패키지 설정파일 포함하여 삭제
  ``` bash
  $ sudo apt-get remove --purge {packageName}
  ```