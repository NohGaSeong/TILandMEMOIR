# EC2-LAMP-ELB 구성하기
## 아키텍처에 구현할 기술
- Linux 기반의 가상서버에 Apache 웹 서버, MySQL 데이터베이스, PHP 어플리케이션을 구축하고 로드 밸런서를 이용하여 이중화 구성을 만듭니다. 

### 필요 AWS 서비스
- Amazon Elastic Compute Cloud(EC2)
- Amazon Virtual Private Cloud(VPC)
- Elastic Load Balancing / Application Load Balancer

### 기타 필요 사항
- Linux O/s
- 간단한 MySQL 및 Query 이해

## 아키텍쳐 구현 순서
### 1. Amazon Linux 2에 LAMP 웹 서버 설치하기
- LAMP 서버 설치 및 테스트
- Custom AMI 생성
- Custom AMI로 두 번째 LAMP 서버 생성
- PuTTY로 SSH 접속하여 데이터베이스 보안 설정

### 2. Application Load Balancer 시작하기
- Load Balancer 유형 선택
- Load Balancer 및 리스너 구성
- Load Balancer에 대한 보안 그룹 구성
- 대상 그룹 구성
- 대상 그룹에 대상 등록
- Load Balancer 생성 및 테스트
- Load Balancer 삭제 선택 사항

`AWS의 대표적인 서비스인 EC2와 LAMP 즉 리눅스 기반의 아팟치 , PHP , MySQL 설치와 접속등을 실습하도록 하겠습니다.`

## EC2 LAMP 구성하기
우선 EC2 시작하기를 눌러 Ec2 생성을 해줍니다.
### 1. AMI 선택
이번 실습은 Linux 환경에서 진행할것이기 때문에 `LInux 2 AMI` 를 선택해줍시다.
### 2. 인스턴스 유형 선택
프리티어인 t2.micro를 선택해줍시다.
### 3. 인스턴스 구성
인스턴스 개수는 `1개` , 서브넷은 `ap-northeast-2a` 나머지는 기본값으로 설정해주시고 아래 `고급 세부 정보`에서 스크립트를 추가해줍시다.

![e1](https://user-images.githubusercontent.com/82383294/136696954-b2c4a242-6f91-4b44-926f-2d510626bfd2.png)

### 4. 스토리지 추가
EC2가 생성됐을때 얼마만큼의 용량을 사용할 것이냐 하는게 기본값으로 내비둡시다.

### 5. 태그추가
이 EC2가 어떤 용도의 EC2인지 구분짓는, 즉 꼬리표 역할을 합니다. 태그 추가를 눌러 키에는 `Name`, 값에는 `lab-web-pub-2a` 이라고 지어줍시다.

### 6. 보안그룹 추가 
기존에 만든 보안그룹이 없기 때문에 `새 보안그룹 생성`를 클릭해줍시다. 이후 보안 그룹 이름을 `lab-web-sg` 으로 변경해주세요. 그리고 웹 테스트를 할 거기 때문에 http 규칙을 추가해줍시다. (소스가 `0.0.0.0/0,::/0` 으로 나올텐데 , 뒤에 부분을 지워주세요.)

### 7. 검토 및 시작
자신이 설정하신 EC2를 확인하신 다음 시작하기를 누르시면 `키 페어 선택 또는 새 키 페어 생성`이 뜨실텐데요 은행의 공인인증서라고 생각하시면 편해요. <br>
키페어 네임은 자유지만 저는 강의를 따라 `seoul-lab-web` 이라고 이름지었어요. 

이러면 인스턴스 생성이 끝나셨어요 와 ~ ! 🤗 이제 이 상태에서 Putty 라는 SSH 접속 툴을 이용해서 EC2 연결하기를 진행해볼게요!

## PuTTY 를 통한 EC2 접속

우선 PuTTY 를 설치하셔야하는데 <a href = " https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html">여기 </a> 서 다운 받으실 수 있어요<br>
이 사이트에 들어가셔서 `Putty.zip` 파일을 다운받습니다.
![e2](https://user-images.githubusercontent.com/82383294/136696955-4da24629-b80c-4288-9682-b8eb56dda659.png)
우선 `PUTTYGEN.ExE` 를 실행하셔서 키페어(pem) 파일을 ppk 파일로 변환시킬건데요. 실행을 시키시고 `load` 클릭. 이후 키페어를 불러오고 `save private key` 버튼을 눌러 `ppk` 파일로 저장시켜줍니다. 

### ssh 로그인
이제 ppk 로 변환을 하셨다면 이 EC2에 SSH 로그인을 해주기 위해 `PUTTY.EXE` 를 실행시켜줍니다. 

실행을 시켜준 후 , `Host name` 에는 ec2의 `public ip` 를 넣어주세요 
![e6](https://user-images.githubusercontent.com/82383294/136696961-863a87bb-f9b0-41a6-be83-b9bb29439af3.png)<br>
이후 `암호와 키`를 설정을 해주셔야하는데 왼쪽의 `ssh` 를 눌러 `auth` 를 클릭해주시고 Browse 버튼을 눌러 `ppk` 파일을 넣으시면돼요
![e5](https://user-images.githubusercontent.com/82383294/136696960-90031dd0-290f-481d-a8d0-9622b4c38185.png)<br>
이후 open 을 누르시면 검은 콘솔창? 비슷한거에 `login-as` 라는 글자가 보이실거에요. 이런 화면이 나온거면 ssh 로그인 화면까지 정상적으로 출력된거에요.

이제 그냥 바로 ec2-user 이라고 입력하시오 엔터를 누르시면!
![e3](https://user-images.githubusercontent.com/82383294/136696956-afdf2b6c-fef2-4050-bb67-4ad5dd667b75.png)<br>
짠! 이렇게 성공적으로 된것을 볼 수 있어요. 이후 인스턴스의 public ip 를 다시 복사하여 브라우저 창에 입력하셔서 이 창이 뜨신다면 성공적으로 리눅스 서버를 할당받아 ssh로 로그인하신거에요!
![e7](https://user-images.githubusercontent.com/82383294/136696962-3facd983-ea33-4c53-a0d7-a3060b768fd9.png)<br>

## Custom AMI(Amazon Machine Image) 생성 및 Custom AMI를 통한 EC2 생성

`지금 생성한 ec2를 가지고 유저데이터로 구성이된 여러분만의 커스텀 AMI 를 만들도록 하겠습니다. `

ec2 인스턴스를 클릭하시고 `작업` -> `이미지 및 템플릿` -> `이미지 생성` 눌러주세요.

### 이미지 생성
`이미지 이름`은 한 눈에 알아볼 수 있도록 `lab-web-202110` 으로 지정했고요, 이름이 이 이미지를 한 눈에 알아볼 수 있게하는 설명과 같기에 `이미지 설명`도 이름과 똑같이 설정했습니다.

#### 재부팅 안함 : 
이 EC2가 정지된 상태에서 이미지 생성을 하겠느냐 아니면 러닝 상태에서 이미지 생성을 하겠느냐의 선택권인데 서비스 중인 EC2 에서 생성을 할때 저걸 체크 안해주면 리붓이 되버려서 안전한 이미지 생성을 위해선 `재부팅 안 함`을 `활성화` 시켜주시면 되겠습니다.

다른 옵션은 안만지고 이미지 생성을 눌러주세요. 잘 만들어졌으면 이미지 -> AMI 를 눌러서 확인해보시면됩니다.

![e8](https://user-images.githubusercontent.com/82383294/136696963-0b9970cd-bd50-4317-97e5-350f979091eb.png)
잘 만들어졌죠? 2~3분 정도만 기다려주시면 `available` 상태가 되니 조금만 기다리면됩니다.

EC2가 지금 2a 로 만들어졌있고 2c로 EC2를 하나 만들건데 그걸 방금 만든 Custom AMI로 만들겁니다.

방금 만든 AMI 를 선택하시고 `시작하기` 를 눌러주세요. 누르시면 인스턴스를 생성했던 화면과 동일한 화면이 뜰건데 2a 와 세팅이 별로 차이가 없기 때문에 금방 끝납니다.

AMI : 시작하기 버튼을 눌렀기에 lab-web-202110 으로 되어있음<br>
서브넷 : 아까와 다른 2c 로 선택
userData : 따로 입력할 필요 x 왜? userData 의 내용이 다 담겨있는 custom AMI 이기 때문.
태그 추가 : Name : Name , Value : lab-web-pub-2c<br>
보안 그룹 : 아까 만든 보안그룹을 똑같이 사용 <br>
키페어 : 아까와 동일<br>

이후 시작하기 버튼을 누르시면 
![e10](https://user-images.githubusercontent.com/82383294/136696966-275576b4-67c6-4afa-8904-45da14d463fe.png)

짠! 잘 생성됐죠? 잘 생성됐는지 확인하기 위해서 2c의 퍼블릭 아이피를 브라우저에 컨 c 컨v를 하면 아래의 화면처럼 잘 출력되는것을 확인할 수 있습니다.
![e9](https://user-images.githubusercontent.com/82383294/136696964-8a34848e-073c-4d1e-8849-baa593f44c2e.png)


## Aplication Load Balancer을 통한 네트워크 이중화 구성

왼쪽에서 `로드 밸런싱 -> 로드 밸런스` 를 클릭해주시고 `로드 밸런스 생성` 을 눌러주세요.

누르시면 3가지의 유형이 나오는데 저희가 사용할 것은 `aplication load balancer `이기 때문에 이것을 선택해줍시다.

### 이름
lab-web-alb<br>
### 스키마(체계)<br>
내부가 아닌 외부 영역을 만들 것이기 때문에 `인터넷 경계`를 선택해줍니다.<br>
### 네트워크 매핑
2a와 2c를 사용할 것이기 때문에 이것들을 선택해주고 서브넷은 기본값을 사용해줄겁니다.<br>
### 리스너
이 alb가 통과할 포트번호를 정의하는겁니다. `HTTP 80` 에 대한 `포트 트래픽`을 허용할 것이기 때문에 그대로 유지해줍니다.
### 태그
Name : Name , Value : lab-web-alb
### 보안그룹 
아래의 사진처럼 alb 보안 그룹을 따로 하나 만들어주시면됩니다.
![e11](https://user-images.githubusercontent.com/82383294/136696967-1c151b57-0f1f-475a-9507-3db45611749a.png)
### 리스너 및 라우팅
어느 EC2를 등록하겠냐하는 타겟그룹을 선택하게되는 만든게 없으므로 새로 하나 만들어줍시다
![e12](https://user-images.githubusercontent.com/82383294/136696968-1234f23a-9b96-4074-b0f9-82977e9aeedb.png)

### 레지스터 타겟
방금 생성한 ec2를 여기 alb에 `타겟그룹`으로 지정하겠다 입니다. 만든 2개의 ec2를 체크하시고 아래에` 보류 중인 것으로 포함`을 누르신 다음 `대상 그룹을 생성`하시면되겠습니다.
![e13](https://user-images.githubusercontent.com/82383294/136696969-cec12c76-d86d-4cf7-9d38-2bff7d3a303e.png)
이후 대상그룹을 적용시키고 `로드밸런서 생성`을 눌러줍시다.
![e14](https://user-images.githubusercontent.com/82383294/136696971-dffb020c-ce56-442b-a45c-59f888e97f80.png)
이제 여기서 가장 중요한게 `DNS name` 입니다. 인터넷에선 ec2로 바로 접근해서 웹페이지를 보는게 아니라 `alb`의 `DNS name` 을 브라우저에 입력해서 생성한 `2개의 ec2`의 웹화면을 보게 할 것입니다. 지금 우리가 한게 그거에요 😆 이제 DNS Name 을 브라우저에 입력하면 짠! 아래의 창이 잘 출력되는 것을 볼 수 있습니다.

![e15](https://user-images.githubusercontent.com/82383294/136696972-4716d68c-49a8-4135-812c-9aefffa08def.png)
분명 `URL 은 퍼블릭 DNS 의 elb` 주손데 불러드린 웹페이지는 `2c`의 가용영역에있는 ec2입니다. 여기서 F5를 눌러보면
![e16](https://user-images.githubusercontent.com/82383294/136696973-40fb4dcf-4c21-4fcf-b2f3-13b3160b5b12.png)
`2a` 가 되었어요. 이러면 `alb` 라고하는 `로드 밸런서`로 2개의 `ec2`가 이중화되어있는 구성이라고 보면되겠습니다.

## 글을 마치며
ㅔ 실습이 좀 길어서 쓰기도 힘들었네요.. 글을 다시 읽어보니까 또 중구난방이긴한데 여러번 쓰다보면 나아질거라고 생각합니다. 끛!
