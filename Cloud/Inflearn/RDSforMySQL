# RDS for MySQL 생성하기

## 1. 아키텍처에 구현할 기술
완전 관리형 MySQL 데이터베이스를 구성하고 Linux 기반의 가상 서버에서 MySQL 클라이언트로 연결합니다.

### 필요 AWS 서비스
- Amazon Relational Database Service(RDS)

### 기타 필요 사항
- 간단한 Query문 및 PHP 문법

## 아키텍쳐 구현 순서
1. RDS for MySQL 구성하기<br>
   (1). Database creation method 선택<br>
   (2). Database Engine 선택<br>
   (3). DB 식별, Master Username/PW 셋팅<br>
   (4). DB Instance size 선택<br>
   (5). 네트워크 설정<br>

2. RDS for MySQL을 EC2에 연결하기.<br>
    (1).PuTTY를 이용하여 Bastion에 SSH 연결<br>
    (2). MySQL 클라이언트를 통해 연결<br>


## Amzaon RDS를 통한 MySQL Database 구성
`AWS의 대표적인 데이터 서비스인 RDS 중에 MySQL 을 생성하는 실습을 해볼거고 EC2에서 MySQL 클라이언트로 RDS for mySQL 접속, 웹 브라우저에서 php 마이 어드민으로 접속해보는 방법을 실습해보도록 하겠습니다.` 

우선 RDS 를 사용하니까 검색창에 RDS 를 검색해 들어가줍시다. 그러면 데이터베이스 생성이라는 버튼이 보이실텐데 그 버튼을 클릭해 데이터베이스 생성을 해주세요. 그리고 읽으면서 따라가시면됩니다.

![d1](https://user-images.githubusercontent.com/82383294/137928262-cddc298e-7590-4a0a-bc47-a1359a06168a.png)
![d2](https://user-images.githubusercontent.com/82383294/137928272-663b2500-1e41-4a31-93e1-5bd4d8a9abed.png)
![d3](https://user-images.githubusercontent.com/82383294/137928220-e4e8844a-ddac-463d-af77-e398f8fe5b59.png)
![d4](https://user-images.githubusercontent.com/82383294/137928226-6559e334-a0eb-43b9-90da-8afab4854bbf.png)
![d5](https://user-images.githubusercontent.com/82383294/137928230-18327ed7-120e-443b-86c8-1066982464e1.png)
![d6](https://user-images.githubusercontent.com/82383294/137928234-fc6fd873-3702-498b-a455-78ac61e4937e.png)
![d7](https://user-images.githubusercontent.com/82383294/137928238-1fc56085-a838-47f0-abe2-f0346e66f1aa.png)    
![d8](https://user-images.githubusercontent.com/82383294/137928244-684b26aa-5cf4-420c-80a2-937463d3436a.png)
<br>
안보여 드린 부분은 그냥 기본값으로 놔두시며됩니다. <br>

옵션 몇 개에 대한 설명을 조금 하도록 하겠습니다.
### 가용성 및 내구성
완전관리형 서비스. 설정으로해서 DB가 마스터,스탠바이 2가지 이중화 구성을 지원. 그래서 `대기 인스턴스 생성`을 선택해주면 마스터 하나와 스탠바이 하나가 이중화 구성이됩니다. 그러면 마스터가 장애가 나도 스탠바이가 있기 때문에 괜찮겠죠? 하지만 실습이기 때문에 만들지 않겠습니다.

### 퍼블릭 엑세스
RDS를 생성했을때 인터넷에서 바로 방화벽이든 보안그룹이든 허용을 해주면 접속이 가능하도록 하겠느냐? 를 설정해주는건데 저희는 실습이기 때문에 `No` 로 설정을 해주겠습니다.

이제 DB 생성을 눌러주세요. 만들어지는데 시간이 조금 걸리기때문에 유튜브 영상 하나 시청하고 오시면 될 것 같습니다.

만들어졌으면 이제 들어가봅시다. 만들어진 DB 를 클릭해주세요.
![d9](https://user-images.githubusercontent.com/82383294/137928252-45708ba0-7313-493d-9688-adb706440808.png)

엔드포인트 : 이 RDS의 DNS 네임이 됩니다. 이후 MySQL 클라이언트로 RDS 접속했을때 이 주소로 접속하게됩니다.

일단 RDS용 보안그룹을 새로 만들어줘야겠죠? 바로 만들러갑시다. RDS 내에서는 보안그룹을 만들 수 있는 창이 따로 없기때문에 EC2 로 넘어가서 왼쪽 메뉴에서 보안그룹을 선택하고 만들어주도록합시다.
![d10](https://user-images.githubusercontent.com/82383294/137928257-b0710163-4654-4fc7-a707-d2fff2e29c06.png)
VPC를 lab-web vpc로 지정해주고 인바운드 규칙을 mysql 로 한다는거 말곤 따로 크게 설정할 게 없어요. 이대로 생성 눌러줍시다.

이후 저희가 만들었던 DB를 누르시고 수정을 누르셔서 보안그룹을 `Default` 에서 저희가 아까만든 `lab-web-rds-mysql-sg` 로 변경해주세요.

## SSH 또는 Web으로 Database 관리를 위한 RDS for MySQL 접속

EC2에 접속해서 mysql 클라이언트라는 명령으로 RDS for MySQL 에 접속하는 방법 하나와 php 마이어드민 라는 소스를 이용해 웹 브라우저에서 rds 정보를 읽어들이는 두 가지 실습을 해볼게요.

우선 DB 만든것을 클릭하시고 엔드포인트를 메모장에 컨c 컨v 를 해줘요. 그리고 EC2에 들어가줍니다.

그러면 저번에 만든 bastion을 클릭하시면 Public IP가 있을텐데 이걸 복사해주세요.

이후 Putty 호스트 네임에 `ec2user@(publicIP)` 를 입력해주시면돼요. ssh auth 를 눌러서 bastion의 ppk 를 선택해줘요.

위에 ec2user 어쩌고 저쩌고를 호스트 네임에 입력해줬기때문에 ec2 user 로그인을 묻지 않고 바로 되게돼요. 

mysql 클라이언트를 접속하기 위해선 

$mysql -u admin -p -h (rdsendpoint) 를 치고 엔터를 누르면 패스워드를 입력하라고 뜰텐데 암호를 그냥 입력하시고 (생각하시는거) 엔터를 누르시면

로그인 성공입니다. 이제 명령어 몇 개를 알려드릴거에요. 이걸 따라 쳐보면서 데이터베이스를 봐보시면됩니당.

데이터베이스 보기
- `show databases;`

데이터베이스 사용
- `use (Database name);`

테이블 보기
- `show tables;`

테이블 검색
- `select *from (테이블명);`

체크를 다 해보시고 나가고 싶다면 exit 를 눌러서 나가시면됩니다. 처음에 ec2를 생성했을때 userdata 로 생성했다면 거기에는 이미 php 마이어드민을 다운받고 컴피그를 실행할 수 있도록 컴퓨 파일까지 이ㅅ을거에요. 근데 그때 안만들어진 RDS 의 정보를 입력하도록 할게요.

지금 디렉토리를 보면 (pwd 입력) `home/ec2-user` 일텐데 `cd/var/www/html/phpMyAdmin` 을 입력해서 요쪽으로 들어가줍시다. 이후 루트 명령을 빌리는 `sudo vi config.inc.php` 를 입력해줘요. 이러면 어드민의 환경파일이 나오는데 cfgs servers host 라는 곳에 localhost 가 있는데 i 를 눌러 insert 모드로 변환해주시고 localhost에 복사했던 rdsendpoint 를 입력해주세요. 다 하셨으면 esc 를 누르고 !wq 로 저장하고 나가주세요. 여기까지해쓰면 PHPMyAdmin 의 환경 설정이 완료된거에요. 이제 브라우저로 가서 테스트를 해봅시다. bastion의 public ip 를 컨c해서 브라우저에 컨 v를 해줍시다. 안 뜰 수도 있는데 보안그룹에 들어가셔서 80에 대한 http 규칙을 추가해주시면됩니다.

php my admin 을 봐야하는데 url 에 `/phpMyAdmin` 을 입력해주시면돼요. 그러면 로그인 화면이 나올텐데 사용자명에는 `admin` , 암호에는 아까 임의로 설정한 암호를 입력해주시면 phpmyadmin 을 통해 rds 로그인이 된거에요 와 ! 왼쪽 메뉴에 mysql을 누르고 user을 누르시면 admin 이라고 하는 유저가 됩니다. 

## 글을 마치며
저번에 만든 bastion 이나 이런 인스턴스들을 비용때문에 다 삭제해버렸는데 그냥 멈춰만 둘 걸 그랬어요 ㅠㅠ 실습을 직접 못따라한게 아쉽지만 글로 기록은 해놨으니 그나마 머리에 박히지 않았을까요? 다음에 시간이 있을때 강의를 처음부터 끝까지 실습만 따라하는 식으로 다시 한번 익혀보겠슴당 히히
