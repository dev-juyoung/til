# nginx 설치
> 해당 문서는 Ubuntu 16.04 LTS 버전을 기반으로 작성했으며, [공식사이트][docs-installation]를 참고하여 작성하였다.

`nginx`는 웹 서버의 한 종류이다.  
대표적인 웹서버인 `Apache`와 양대산맥을 이룬다.  
~~(개인적인 생각)~~

웹 서버란, 클라이언트(웹 브라우저)의 요청을 처리하기 위한 서버쪽 파트의 소프트웨어라고 볼 수 있으며, `HTTP통신`을 이용하여 클라이언트와 정해진 규격으로 정보를 주고 받을 수 있다.

### \#. 서명키 추가.

nginx 설치 중, PGP키의 누락으로 인한 오류 문구를 해결하기 위해, 우선 서명키를 생성하고, `apt의 keyring`을 추가하는 단계가 필요하다.  

서명키는 [해당 사이트][signing-key]를 통해 제공받을 수 있으며,  
원하는 위치에 `nginx_signing.key`와 같은 파일명으로 생성해 두면 된다.

``` bash
$ sudo apt-key add {path}/nginx_signing.key
```

### \#. 패키지 인덱스정보 추가.

``` bash
# vi를 이용하여 /etc/apt/sources.list에 추가.
deb http://nginx.org/packages/ubuntu/ {codename} nginx
deb-src http://nginx.org/packages/ubuntu/ {codename} nginx
```

해당 커맨드 명령에서, `codename`에 해당하는 부분은 [참고사이트][docs-codename]를 확인하여 원하는 버전을 사용하면 된다.

### \#. 패키지 인덱스정보 갱신 및 설치

``` bash
$ sudo apt-get update
$ sudo apt-get install nginx
```

[docs-installation]: https://nginx.org/en/linux_packages.html
[signing-key]: https://nginx.org/keys/nginx_signing.key
[docs-codename]: https://nginx.org/en/linux_packages.html#distributions