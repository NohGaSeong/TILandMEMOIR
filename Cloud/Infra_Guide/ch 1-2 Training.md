# 실습
## AWS 인스턴스 생성
### EC2 인스턴스 생성

1. AWS에 로그인해준다. 이후 리전을 서울로 설정해주세요!
2. 인스턴스 생성을 누르면 아래와 같은 AMI 창이 뜨실텐데 프리티어를 제공해주는 Amazon Linux 를 사용할게요
![2-1번](https://user-images.githubusercontent.com/82383294/141995427-45b6e1e7-a09d-4bcd-ae79-4e7ac5b9d7e3.png)

3. EC2 의 유형은 `t2.micro` 프리티어를 지원해주기에 이걸 사용했어요. (굳이 크게 할 필요도 없고요)
![2-2번](https://user-images.githubusercontent.com/82383294/141995429-24071eb1-6f7b-48f5-8ae9-270a80f1ff4f.png)

4. 스토리지는 딱히 건들게 없기에 기본값으로 놔둬줬어요.
![2-3번](https://user-images.githubusercontent.com/82383294/141995431-aa1a0bc8-ebd5-4da2-addc-f1a0c1931cc9.png)

5. 태그는 Name 태그만 만들게요. 이 인스턴스가 어떤 역할을 하는지 이름을 지어주는거라고 생각하면 편해요.
![2-4번](https://user-images.githubusercontent.com/82383294/141995433-bb7b567b-7ea1-4063-95c5-28326ee3d897.png)

6. 인스턴스에 대한 접근을 제어하기 위한 `보안 그룹` 화면이에요. 보안그룹은 `새 보안 그룹`을 만들어줄게요 

  보통 회사 IP만 지정하는 것이 좋고, 정말 필요한 IP 주소와 포트 번호에 대해서만 접속을 허용하는 것이 중요하다고해요.
  
![2-5번](https://user-images.githubusercontent.com/82383294/141995434-1edd1eaa-74b0-40ae-9dde-9f929aa968a6.png)

이후 다 만드셨으면 `검토 및 시작` 버튼을 눌러 자기가 설정을 잘 했는지 한번 확인을 해주시고 인스턴스를 만들어주세요. 
![2-6 번](https://user-images.githubusercontent.com/82383294/141995435-05b00fac-0a69-4266-922b-310a9ad1c177.png)

7. 키페어도 만들어야하실텐데 이 서버에 접속할 수 있는 <b>열쇠</b> 라고 생각하시면 좋아요. 잃어버리면 다시 다운 받지 못하니까 안전하게 보관해주세요!
![2-7번](https://user-images.githubusercontent.com/82383294/141995436-0c642fe2-ad27-4c4e-b320-da0c526aee26.png)

8. 이제 그렇게 생성을 하고 조금 기다려주시면 이렇게 인스턴스가 만들어져요 와! (짝짝)
![2-8번](https://user-images.githubusercontent.com/82383294/141995390-036fec1f-a3af-4960-a2a3-ead8e4dcf441.png)

이제 저희가 만든 인스턴스를 조금 살펴볼까요? DNS,IP와 관련된 항목을 확인하면 인스턴스에 퍼블릭, 프라이빗 도메인과 IP 주소가 각각 할당됐음을 알 수 있어요. 해당 도메인과 IP를 이용해 이 인스턴스에 접근할 수 있어요.

퍼블릭 도메인과 IP는 별도의 설정을 하지 않는 이상 인스턴스가 꺼질 때 사라지고 다시 켜질 때마다 새로 할당받아요.

중요! : <b>켜져있으면 계속 요금 나가니까 사용안하실때는 인스턴스를 중지하는 습관을 가져주세요!</b>

### EC2 인스턴스 접속
제가 예전에 쓴 <a href = "https://github.com/NohGaSeong/TIL/blob/main/Cloud/Ec2-Lamp-Elb.md">TIL</a> 을 참고해주세요!

### HTTP,HTTPS 도 접근 가능하도록 보안 그룹 추가하기
현재 인스턴스에는 ssh 포트마 허용해 놓았기 때문에 https.http 의 기본포트이 80,443 포트로 접속을 시도하면 동작하지 않아요. 웹요청을 받기 위해선 이 두 개의 포트로 요청을 받을 수 있개 허용해야해요.

왼쪽 EC2 메뉴에서 '네트워크 및 보안' -> '보안 그룹' 메뉴를 차례로 선택한 뒤 '보안 그룹 생성' 버튼을 클릭해요. HTTP와 HTTPS를 열어둔 보안그룹을 생성하고 (SSH 를 했던 것처럼 하시면돼요)인스턴스를 우클릭. 이후 네트워킹->보안 그룹 변경 메뉴를 선택해주시고 만든 보안그룹을 적용시켜주세요.
![4-1](https://user-images.githubusercontent.com/82383294/141995422-89aee876-ea4c-4df4-b806-a066bad74426.png)

아래 사진처럼 만드시고 적용시키면돼요.

## 샘플 프로젝트를 실행하기 위한 서버 환경 구성
다음으로 생성한 EC2 인스턴스에서 간단한 샘플 웹 애플리케이션을 서비스해볼게요. 서비스할 애플리케이션은 Node.js로 만들어졌기에 서버에 Node.js를 설치해야해요

```
  # nvm을 설치하는 스크립트 파일을 인터넷에서 내려받아 실행한다.
  # nvm은 node version manager로서 원하는 버전의 노드를 설치 및 관리할 수 있는 애플리케이션이다.
  $ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh ¦ bash
  
  # 내려받은 nvm 설치 스크립트를 실행한다.
  $ .~/ .nvm/nvm.sh
  
  # nvm을 이용해 node.js 10.13.0 버전을 설치한다.
  $ nvm install 10.13.0
  
  # 설치한 Node.js 버전이 올바르게 설치됐는지 확인한다.
  $ node -e "console.log('Running Node.js ' + process.version)"
  
  
```

## 소스코드 배포
### Git으로 EC2인스턴스에 코드 배포하기

```
  #시스템 패키지를 설치할때는 root 권한이 필요함
  $ sudo yum install curl-devel gettext-devel openssl-devel zlib-devel
  
  ..
  
  # 다운로드를 진행할지 묻는다. yes를 의미하는 y를 입력한다.
  
```
1. yum 패키지 매니저를 이용해 git에 필요한 패키지를 다운받아요.
2. 소스코드를 배포할 디렉터리를 생성해요.
```
  $ cd /var
  
  # mkdir 명령어를 이용해 소스코드를 배포할 디렉터리를 생성해요.
  # 이떄 sudo를 이용해 root 권한으로 명령어를 실행하게 되는데, 이는 /var 디렉터리의 소유권한이 root로 돼있기 때문에
  # 해당 디렉터리에 파일이나 디렉터리를 추가하기 위해서는 root 권한이 필요하기 떄문이에요.
  
  $ sudo mkdir www
  
  # 코드 관리는 일반 유저인 ec2-user 로 처리할것이기에 /var/www 경로를 ec2-user의 소유로 변경해요
  
  $ sudo chown ec2-user www
```

3. 이제 Git을 이용해 Git 저장소에 있는 소스코드를 내려받아요. 샘플 프로젝트는 Git 저장소인 깃허브에 공개돼 있으므로 해당 ㅡㅍ로젝트를 그대로 내려받아요.
```
  $ cd /var/www
  
  # /var/www/aws-exercise-a 경로에 소스코드를 다운받게돼요.
  $ git clone https://github.com/deopard/aws-exercise-a.git
  $ cd aws-exercise-a
```

4. 애플리케이션을 실행하기 위해 프로젝트의 의존성 패키지를 설치해요
`$ npm install`

## 웹 서버와 웹 애플리케이션 서버
### nginx,Phusion Passenger 설치 및 서비스
1. ec2 인스턴스 접속
2. Phusion Passenger의 설치파일 다운
```
  # Phusion Passenger 설치 파일을 내려받기 위해 /var/www 경로로 이동
  $ cd /var/www
  
  # wget 명령어를 이용해 웹에 있는 파일로 로컬을 내려받아요.
  # 이때 파일 주소를 보면 Phusion Passenger도 파일을 호스팅하는데 AWS를 사용하고있어요.
  $ wget http:/s3.amazonaws.com/phusion-passenger/releases/passenger-5.3.6.tar.gz
  
  # sudo 명령어를 통해 루트 권한으로 /var/passenger 디렉터리를 생성해요.
  # 루트 권한이 필요한 이유는 /var 디렉터리가 루트 계정의 소유로 돼 있기 떄문이에요
  $ sudo mkdir /var/passenger
  
  # passenger 파일을 ec2-user로 처리할거라 chown 명령어로 /var/passenger 디렉터리의 소유자를 ec2-user로 변경해요
  # 현재 디렉터리 쇼유자 = 루트 , 루트 권한 이용해야겠죠?
  $ sudo chown ec2-user /var/passenger
  
  # 내려받은 passenger 설치 파일을 /var/passenger 경로에 압축을 풀어줘요.
  $ tar -xzvf passenger-5.3.6.tar.gz -C /var/passenger
```

3. rvm을 설치해요. 루비 버전 매니저인데 phusion passenger 가 C++과 루비로 만들어져서 루비를 설치해줄게요.ㅓ
```
  # curl 명령어를 이용해 공개키를 내려받아요. 이 키는 내려받으려는 rvm 패키지가 유효한 패키지인지 확인해줘요.
  $ gpg --keyserver hkp://pool.sks-keyservers.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
  
  # stable 버전의 rvm을 내려받아요
  $ curl -sSL https://get.rvm.io ¦ bash -s stable
  
  # rvm 명령어를 현재 터미널 세션에서 사용할 수 있게 해요
  $ source /home/ec2-user/ .rvm/scripts/rvm
  $ rvm reload
  
  # 루비를 설치하는데 필요한 라이브러리등을 설치해요
  $ rvm requirements run
```
4. 루비를 설치해줘요
`$ rvm install 2.4.3`

5. Passenger 명령어를 쉽게 실행하기 위한 변수를 설정하는 작업을 해줘요.
```
  # 설치된 Passenger의 경로를 $PATH 변수에 넣어줘요. 그럼 전체 경로를 입력할 필요가 없이 Passenger 명령어만 입력해주면돼요.
  $ echo export PATH=/var/passenger/passenger-5.3.6/bin:$PATH >> ~/.bash_profile
  
  # 업데이트된 bash shell의 설정 파일을 현재 ㅓ미널 세션에서 바로 사용할 수 있게해줘요.
  $ source ~/.bash_profile
```

6. Phusion Passenger 를 이용해 Passenger nginx module을 설치해줘요
```
  $ passenger-install-nginx-module
  
  (대충 설명들)
  
  <enter>
  
  # Node.js 로 이루어진 샘플 프로젝트이기에 Node.js 말고 다 해체. 체크박스가 잘 안보이면 설명대로 ! 를 눌러주자

  <enter>
  
  (경고 메세지들. 가상 메모리 부족해서 설치 시 문제가 발생할 수도 있다는 뜻)
  
  # 컨c를 눌러서 설치 그만하고 가상 메모리를 늘립시다.
  
  $ sudo dd if=/dev/zero of=/swap bs=1M count=1024
  $ sudo mkswap /swap
  $ sudo swapon /swap
```

7. 다시 설치를 시도해줘요 
```
  $ passenger-install-nginx-module
  
  (그럼 nginx 까지 자동으로 설치할거냐고 묻는데  1 누르고 엔터)
  (설치 위치 묻는데 그냥 엔터)
  (경고 메시지 읽고 Installer에서 권장하는 방법으로 rvmsudo를 실행해 installer을 다시 실행)
  $ export ORIG_PATH="$PATH"
  $ rvmsudo -E /bin/bash
  # export PATH="$ORIG_PATH"
  # export rvmsudo_secure_path=1
  #  /home/ec2-user/ .rvm/gems/ruby-2.4.3/wrappers/ruby /var/passenger/passenger-5.3.6/bin/passenger-install-nginx-module
  
  # 엔터
  # 1 엔터
  #엔터
  
  (그러면 정상적으로 설치된다)
  (그러면 nqinx의 설정 파일의 경로를 알려주고 Phusion passenger와의 연동을 위한 설정도 installer에서 추가했음을 알려줘요)
  
  (엔터)
  # exit 
```

8. 텍스트 편집기로 nginx의 설정을 변경하기 위해 파일을 연다. 
`$ sudo vi /opt/nginx/conf/nginx.conf`

9. http요소의 첫줄에 server_names_bucket_size 설정을 추가한다.
```
  http {
    # 긴 서버 네임 허용
    server_names_hash_bucket_size 256;
    passenger_root /var/passenger/passenger-5.3.6;
    passenger_ruby /home/ec2-user/ .rvm/gems/ruby-2.4.3/wrappers/ruby;
    
    ..
    
```

10. server 요소의 설정도 다음과 같이 수정해요.
```
  server {
    li
