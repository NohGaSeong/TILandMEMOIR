#실습
## nginx, Phusion Passenger 서비스 명령어 추가

1. `_`/etc/init.d 경로에 스크립트를 추가한다. init.d는 서비스 스크립들이 존재하는 경로다.
```
  $ cd /etc/init.d
  
  # 텍스트 에디터를 이용해 nginx 파일을 생성, 수정한다.
  $ sudo vi nginx
```

2. nginx 시작 스크립트의 내용을 복사 및 붙여넣기해서 저장한다.
3. 실행 가능한 서비스로 만들기 위해 파일 권한을 변경한다.
` $ sudo chmod 755 nginx `

4. 이제 다음과 같이 손쉽게 nginx 서비스를 조작할 수 있다.
```
  # nginx 종료
  $ sudo service nginx stop
  Stopping ngix:    [OK]
  
  # nginx 시작
  $ sudo service nginx start
  Starting nginx:   [OK]
  
  # nginx 재시작
  $ sudo service nginx restart
  nginx : the configuration file /opt/nginx/conf/nginx.conf syntax is ok
  nginx : configuration file /opt/nginx/conf/nginx.conf test is successful
  Stopping nginx :           [ok]
  Starting nginx :           [ok]
  
  # nginx 프로세스 확인
  $ sudo service nginx status
  nginx (pd 7249 7245) is running...
```
## 시스템 시작시 자동 시작 서비스에 등록
서버 인스턴스가 켜져도 샘플 애플리케이션을 실행하기 위한 nginx, Phusion passenger가 실행되지 않으면 서버가 켜질 때마다 접속해서 서비스를 실행해야해요. 
서버가 한 대라면 조금 귀찮은 정도겠지만 나중에 여러대의 서버를 돌리고 트래픽에 따라 서버가 자동으로 켜지고 꺼진다면 큰 문제가 되겠죠?  

1. 서버가 켜지면 자동으로 nginx 서비스가 실행되도록 시작 서비스에 등록한다.
```
  #시작 서비스 관리를 위한 툴인 ckconfig를 이용해 nginx 스크립트를 chkconfig에서 관리하는 서비스로 등록한다.
  $ sudo chkconfig --add nginx
  
  # 시작 서비스에 쉽게 등록하기 위해 runlevel 을 GUI 로 관리할 수 있게 해주는 ntsysv 명령어를 실행한다.
  $ sudo ntsysv
  
```

2. 화면에서 nginx 를 체크하고 확인을 선택하세요. 체크는 (space) ,이동은 (tab) 키를 사용하시면돼요.

## 하나의 서버에서 두 개의 에플리케이션 서비스하기
앞에서는 하나의 애플리케이션만 서비스했지만 한 서버에 여러가지 애플리케이션을 실행하는 경우도 많겠죠? 이번에는 nginx를 이용해 한 서버에서 두 개의 다른 애플리케이션을
서비스 해볼게요.

하나의 서버는 하나의 IP 주소를 갖게 되지만 그 IP 주소에 여러 개의 도메인을 연결 할 수 있어요. 따라서 하나의 서버라도 여러 개의 주소를 가질 수 있게 되는 것이에요.
서버 내의 있는 nginx가 어떤 주소로 요청했는지 파악해서 올바른 애플리케이션에 전달할 수 있ㅇ요. 이 경우에는 nginx가 라우터의 역할을 하게 되는것이죠.

1. 앞서 배포했던 것과 다른 애플리케이션 코드도 서버에 배포할게요. git으로 b 프로젝트를 배포해볼거에요. 배포과정은 동일해요
```
  $ cd /var/www
  $ git clone https://github.com/deopard/aws-exercise-b.git
  $ cd aws-exercise-b
  $ npm install
```

2. 텍스트 편집기로 nginx의 설정을 변경하기 위해 파일을 열어요
` $ sudo vi /opt/nginx/conf/nginx.conf `

3. 이전에는 nginx에서 서버를 구분하기 위해 EC2인스턴스의 IPv4 퍼블릭 주소를 sever_name으로 사용했지만 이번에는 EC2 인스턴스의 퍼블릭 DNS를 사용해요. 파일을 수정한 뒤 저장해주세요.
```
  # 기존에 추가한 server 요소
  server{
    ..  
    server_name <EC2 인스턴스의 IPv4 퍼블릭 주소>;
    ..
  }
  
  # 기존 설정에 새로운 server 요소를 하나 더 추가한다.
  server{
    listen 80;
    # 이 서버에는 도메인 주소를 입력해서 기존에 추가한 서버와 구분한다.
    server_name <퍼블릭 DNS(IPv4)>;
    
    root /var/www/aws-exercise-b/public;
    
    passenger_enabled on;
    passenger_app_type node;
    passenger_startup_file /var/www/aws-exercise-b/app.js;
  }
```

4. 변경된 설정을 적용하기 위해 nginx,Phusion Passenger 서비스를 재시작해요.
`$ sudo service nginx restart`

5. 브라우저에서 EC2 인스턴스의 IP주소와 DNS주소로 접속할 때 다른 애플리케이션이 실행되는 것을 확인해요.

## 정리
- 운영 서버 아키텍처에 서버와 클라이언트가 어떤 식으로 구성될 수 있는지 알 수있다.
- 각 구성방법의 장단점을 알 수 있다.
- AWS EC2를 이용해 인스턴스 생성부터 해당 인스턴스 내에 애플리케이션 코드를 실행할 수 있는 서버 환경을 구축할 수 있다.

 


