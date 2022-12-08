# Ngnix 란?
- 엔진엑스(Nginx)는 Igor Sysoev라는 러시아 개발자가 개발한 동시접속 처리에 특화된 웹 서버 프로그램이다.
- Apache보다 동작이 단순하고, 전달자 역할만 하기 때문에 동시접속 처리에 특화되어 있다.
- 동시접속자(약 700명) 이상이라면 서버를 증설하거나 Nginx 환경을 권장한다고 한다. 지금은 아파치가 시장 점유율이 압도적(?)이지만, 아마존웹서비스(AWS) 상에서는 시장 점유율 44%에 달할정도로 가볍고, 성능이 좋은 엔진이라고 한다.

## 웹서버(nginx)의 역할?
### 1-1. 정적 파일을 처리하는 HTTP 서버로서의 역할
웹서버의 역할은 HTML, CSS, Javascript, 이미지와 같은 정보를 웹 브라우저(Chrome, Iexplore, Opera, Firefox 등)에 전송하는 역할을 한다. (HTTP 프로토콜을 준수)

### 1-2. 응용프로그램 서버에 요청을 보내는 리버스 프록시로서의 역할
- 두번째 역할은 리버스 프록시(reverse proxy)인데, 한마디로 말하면 클라이언트는 가짜 서버에 요청(request)하면, 프록시 서버가 배후 서버(reverse server)로부터 데이터를 가져오는 역할을 한다. 
- 여기서 프록시 서버가 Nginx, 리버스 서버가 응용프로그램 서버를 의미한다.
- 웹 응용프로그램 서버에 리버스 프록시(Nginx)를 두는 이유는 요청(request)에 대한 버퍼링이 있기 때문이다.
- 클라이언트가 직접 App 서버에 직접 요청하는 경우, 프로세스 1개가 응답 대기 상태가 되어야만 한다. 따라서 프록시 서버를 둠으로써 요청을 배분하는 역할을 한다.
  - nginx.conf 파일에서 location 지시어를 사용하여 요청을 배분한다.
- Nginx는 비동기 처리 방식(Event-Drive) 방식을 채택하고 있다.
  - 동기(Synchronous) : A가 B에게 데이터를 요청했을 때, 이 요청에 따른 응답을 주어야만 A가 다시 작업 처리가 가능 (하나의 요청, 하나의 작업에 충실)
  - 비동기(Asynchronous) : A의 요청을 B가 즉시 주지 않아도, A의 유휴시간으로 또 다른 작업 처리가 가능한 방식

## ngnix 설치하기
```
sudo apt-get install nginx # 설치
sudo apt-get remove nginx # 제거
nginx version: nginx/1.13.2
sudo find / -name nginx.conf #경로 찾기
```
## ngnix 파일구조
```
├── conf.d # (디렉토리) nginx.conf에서 불러들일 수 있는 파일을 저장
├── fastcgi.conf # (파일) FastCGI 환경설정 파일
├── fastcgi_params
├── koi-utf
├── koi-win
├── mime.types
├── nginx.conf # 접속자 수, 동작 프로세스 수 등 퍼포먼스에 관한 설정들
├── proxy_params
├── scgi_params
├── sites-available # 비활성화된 사이트들의 설정 파일들이 위치한다.
│   └── default
├── sites-enabled # 활성화된 사이트들의 설정 파일들이 위치한다. 존재하지 않은 경우에는 디렉토리를 직접 만들 수도 있다.
│   └── default -> /etc/nginx/sites-available/default
├── snippets
│   ├── fastcgi-php.conf
│   └── snakeoil.conf
├── uwsgi_params
└── win-utf
```
## ngnix 설정하기
4-1. 최상단 (Core 모듈)
user  nginx; # (디폴트값 : www-data) 
worker_processes  1;
error_log  /var/log/nginx/error.log warn;
pid        /var/run/nginx.pid;
user : NGINX 프로세스가 실행되는 권한

nginx는 마스터(master)와 워커(worker) 프로세스로 나뉜다.

워커 프로세스가 실질적인 웹서버 역할을 수행한다.

user 지시어는 워커 프로세스의 권한을 지정한다.

워커 프로세스를 악의적 사용자가 제어하면 해당 머신을 최고 사용자의 권한으로 원격제어하는 것이기 때문에 위험하다.

본 포스팅에서는 nginx로 변경하였다.

work_processes : NGINX 프로세스 실행 가능 수

위에서 언급한 워커 프로세스이다. 실질적인 웹서버 역할을 한다.

auto도 무방하지만, 명시적으로 서버에 장착되어 있는 코어 수 만큼 할당하는 것이 보통이며, 더 높게도 설정 가능하다.

pid : NGINX 마스터 프로세스 ID 정보가 저장된다.

4-2. events 블락
events { 
    worker_connections  1024;
    # multi_accept on; (디폴트값 : off) 
}
NGINX의 특징인 비동기 이벤트 처리 방식에 대한 옵션을 설정한다.

worker_connections는 하나의 프로세스가 처리할 수 있는 커넥션의 수를 의미한다.

최대 접속자수 = worker_processes X worket_connections가 된다.

4-3 http 블락
http { 
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;
 
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    '$status $body_bytes_sent "$http_referer" '
    '"$http_user_agent" "$http_x_forwarded_for"';
 
    access_log  /var/log/nginx/access.log  main;
 
    sendfile        on;
 
    #tcp_nopush     on; 
 
    keepalive_timeout  65;
 
    #gzip  on; 
 
    include /etc/nginx/conf.d/*.conf;
}
 
keepalive_timeout : 접속시 커넥션을 몇 초동안 유지할지에 대한 설정값. 이 값이 높으면 불필요한 커넥션(접속)을 유지하기 때문에 낮은값 또는 0을 권장한다. (default=10)

servers token : NGINX의 버전을 숨길것인가에 대한 옵션이다. 보안상 주석을 제거하여 설정하는 것이 좋다.

types_hash_max_size, server_names_hash_bucket_size 호스트의 도메인 이름에 대한 공간을 설정하는 것으로 이 값이 낮을 경우 많은 가상 호스트 도메인을 등록한다거나, 도메인 이름이 길 경우 bucket 공간이 모자라 에러가 생길 수 있으므로 넉넉하게 설정한다.

4-4 기타
include 옵션 : 가상 호스트 설정이나 반복되는 옵션 항목을 inlcude를 통해 불러올 수 있다. EX) 리버스 프록시를 각 도메인에 설정한다고 했을 떄 헤더 처리 옵션등을 conf.d 디렉토리에 넣어두고 incldue 명령을 통해 불러올 수 있다.

4-5 설정 파일의 반영
설정 파일의 내용을 변경한 후에는 NGINX에 반영해야 하는데, reload 명령을 이용한다.

sudo service nginx reload;
