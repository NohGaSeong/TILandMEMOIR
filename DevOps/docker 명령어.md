# Docker 명령어
- Docker는 os 의 자원을 사용하기 떄문에 기본적으로 root 사용자에게 명령어를 사용해야함.
## CentOS
1. search (image 검색)
- docker hub 로부터 사용가능한 image 를 찾는 명령어
- docker 는 docker hub를 통해 github처럼 사용자들간의 이미지 공유를 할 수 있는 환경이 구축되어있다.
- 공식 이미지는 galid/centos 처럼 / 앞에 사용자의 이름이 붙지 않음.
2. pull(image 다운로드)
- docker hub로 부터 image를 다운받는 명령어
3. images(image 목록보기)
- 현재 Host PC에 다운 받아져있는 image 를 출력하는 명령어

4. run
- (docker run<옵션><이미지이름 or 이미지 ID><실행할 파일>)
- 메인으로 실행되는 파일이 종료되면 컨테이너도 같이 종료됨, 따라서 계속해서 컨테이너를 유지하고 싶다면 -d 옵션을 이용해야함.
- 다운받은 image 를 실행한 형태인 컨테이너로 만드는 명령어이다.
- 옵션?
    - -i : 사용자가 입출력을 할 수 있는 상태로 한다.
    - -t : 가상 터미널 환경을 에뮬레이션 하겠다는 말
    - -d : 컨테이너를 일반 프로세스가 아닌 데몬프로세스 형태로 실행하여 프로세스가 끝나도 유지되도록 한다.
- 컨테이너 종료
    - Ctrl + d : 메인 실행파일인 쉘이 종료되기 때문에 컨테이너도 같이 종료된다.
    - Ctrl p + q : 컨테이너가 백그라운드에 살아있는 채로 host OS 로 돌아간다.
5. ps
- 실행중인 컨테이너의 목록을 확인한다.
- -a : 이전에 종료되었던 컨테이너들을 포함한 컨테이너의 목록을 확인한다.
6. start
- 컨테이너를 실행한다.
7. attach
- docker ps 를 통해 현재 실행중인 컨테이너 목록을 확인한다.
8. stop
- docker stop "Container ID"
9. rm
- 운영체제의 프로세스와 달리 컨테이너가 종료되더라도 다시 실행하면 이전 상태가 유지된다. 따라서 사용하지 않는 컨테이너는 rm 명령어를 통해 완전히 제거를 해야한다.
10. port forwarding
- 'docker run -it -p "HOST PORT":"Docker PORT""실행할 도커 이미지"/bin/bash
11. docker create image
- 반드시 "Dockerfile" 이라는 이름으로 Docker file 생성
## Ubuntu
1. 실행
    - docker run -it --name ubuntu docker.io/ubuntu/bin/bash
2. 기본 설정
    1. service 명령어 이용
        - apt-get update, apt-get upgrade
    2. 네트워크 명령어 이용(ip add)
        - apt-get install -y net-tools