# SSL 인증서 설정

요즘은 네트워크 통신을 함에 있어, 조금 더 보안적으로 안전함을 위해 대부분의 서비스들이 `HTTPS`를 사용하고 있다.


하지만, 이러한 `HTTPS`를 지원하기 위해서는 `SSL인증서`라는 것을 구매하여야 하며, 이 인증서가 그렇게 싼 가격은 또 아니기 때문에, `개인 프로젝트` 또는 `스타트업`에서는 금전적 부담을 느낄 수 밖에 없다.

이러한 금전적 부담이 `HTTPS`의 확산을 지연시키고 있다라는 생각에 `Mozilla`, `Cisco`, `EFF`, `Google`등 다수의 대기업들이 참여하여 무료로 `SSL 인증서`를 발급받고 `HTTPS`를 사용할 수 있도록 `Let's Encrypt`를 내놓았다.

해당 문서에서는 `Let's Encrypt`를 조금 더 편리하게 설정할 수 있는 클라이언트 프로그램인 `Certbot` 이라는 녀석을 이용하여 `SSL 인증서`를 발급하고 웹 서버인 `Nginx`에 설정하여 `HTTPS` 통신을 할 수 있는 방법에 대해 정리해보고자 한다.

### \#. 필수 준비물
* Ubuntu.
* Nginx.
* SSL 인증서를 발급할 도메인 주소.

우선, SSL인증서를 발급하기 위한 도메인 주소는 필수이며, 본인의 OS나 서버가 다르다 하더라고 [공식페이지][certbot]에서 본인의 환경에 맞도록 `Certbot`을 설치하여 진행하면 된다.

### \#. Certbot 설치
``` bash
$ sudo apt-get update
$ sudo apt-get install software-properties-common
$ sudo add-apt-repository ppa:certbot/certbot
$ sudo apt-get update
$ sudo apget-get install python-certbot-nginx
```

우선 저장소 목록을 최신으로 update 한 후, `add-apt-repository` 명령어를 통해, certbot 저장소를 추가하여 주고, `nginx`용 플러그인이 설정되어 있는 `certbot`을 설치한다.

### \#. Nginx 설정파일 변경.
``` bash
# /etc/nginx/conf.d/default.conf
server {
    #other code...

    listen 80;
    listen [::]:80;

    # 해당 서버의 도메인 주소를 설정한다.
    server_name example.com;

    #other code...
}
```
특별하게 설정을 변경하지 않았다면, 기본적으로 `/etc/nginx` 하위에 설정파일이 존재한다.

기본적으로 설정되어 있는 `80포트 (http)`의 server block 내에서 `server_name` 필드를 찾아 설정하고자하는 도메인 주소로 변경한 후, 저장한다.

``` bash
$ sudo nginx -t # nginx 설정파일 테스트.
$ sudo service nginx reload # nginx 서비스 재시작.
```
> 만약 `sudo nginx -t`의 과정에서 테스트에 통과하지 못한 경우, 오류 로그에 어디에서 설정이 잘못되었는지 나오므로 출력 로그를 유심히 확인하도록 한다.

### \#. SSL 인증서 발급
``` bash
$ sudo certbot --nginx -d example.com
```
위의 명령어 한줄만 입력하면 `SSL 인증서`를 발급 받을 수 있다.

만약, `example.com` 이 외의 도메인도 사용하고 싶다면 `-d` 옵션과 함께 도메인을 입력하면 된다

``` bash
$ sudo certbot --nginx -d example.com -d www.example.com -d dev.examplecom ...
```

해당 명령어를 입력하면 `command line`을 통해 몇가지 추가적인 대화형 질/답을 통해 설정을 진행할 수 있다.

질문의 내용은 대략적으로 다음과 같다.
* SSL 인증서 만료 등 긴급상황을 대비하여 통지받을 Email 주소.
* 최초 등록이라면 서비스 이용약관에 대한 동의.
* 등록된 이메일로 새로운 소식등에 대한 메일 발송 유무.
* 모든 요청에 대하여 `https`로 redirect 유무.

### \#. SSL 인증서 갱신
유료로 발급되는 SSL 인증서 또한 만료일이 지정되어 있지만, `Let's Encrypt`는 무료라는 장점이 있는데 반해, 90일 이 후 만료라는 아쉬움점도 있다.

하지만 `Certbot`을 이용하면, 단 한줄의 명령어를 통해 특별한 문제가 없을 경우, 갱신 처리가 가능하다.

실질적으로 갱신 처리가 제대로 되는지 확인 할 수 있으면 좋겠지만, `Let's Encrypt`는 만료일이 1달 이내인 인증서에 대해서는 갱신처리가 가능하므로, 우선은 추후 갱신에 문제가 없을지에 대한 테스트 정도만 진행하도록 한다.

``` bash
$ sudo certbot renew --dry-run
```

Certbot의 `renew` 라는 명령어를 통해 인증서를 갱신 할 수 있으며, `--dry-run` 옵션을 통해, 실질적으로 인증서를 갱신하진 않지만, 갱신 시, 추가적인 문제가 발생하는지에 대한 여부를 테스트할 수 있도록 지원하고 있다.

[certbot]: https://certbot.eff.org/