# Systemd 주요 역할
## 주요 역할
- 기존 init 프로세스의 기능을 지원 및 통합
- 동작 모드에 따른 시작 서비스 관리
- 병렬 실행 및 종속성 모델 과닐
- 커널 로그 엔트리 관리
- 네트워크 연결 관리
- 로그인 관리

## Unit , Unit 파일
- systemd가 관리하는 기본 개체 단위
- unit 유형
  - service, socket, device, mount, automount, swap, target,path, timer, slice, scope
  - unit 파일의 suffix로 활용
- Unit 별로 수행할 작업의 정의나 설정은 unit 에 정의
### Unit 파일 형식 (INI 파일 형식)
- Unit 섹션 : Unit의 기본 정보 정의
  - Description : 사람이 읽을 수 있는 Unit 정보. 레이블로 활용
  - After, Requires, Wants : Unit의 종속성을 지정

- Unit 유형 섹션: Unit 유형에 따른 속성들 정의
  - ExecStart : 구동할 명령어를 지정(절대 경로 활용)
  - Restart : 서비스 재시작 여부 지정
 
- Install 섹션 : Unit 설치와 관련된 정보 정의
  - Alias : Unit을 등록할 때 사용하는 이름
  - WantedBy : Unit간 종속성 지정

## Systemd 좀 더 알아보자.
### systemctl
- systemd의 상태를 조사하고 설정을 변경하는데 사용되는 도구.
- 자주 사용하는 systemctl 서브 커맨드들은 아래와 같다.
```
list-unit-files : 설치된 Unit 목록 화인
enable unit : unit이 부팅 시 자동 활성화
disable unit : unit이 부팅 시 자동 활성화 되는 것을 방지
isolate target : 타겟의 실행 모드를 변경
start unit : unit 을 즉시 활성화
stop unit : unit을 즉시 비활성화
restart unit : unit 을 재시작. 실행되지 않은 상태였다면 start
status unit : unit의 상태 및 최근 로그 내용을 확인
kill pattern : 패턴과 일치하는 unit에 시그널을 보냄
reboot : 컴퓨터를 재 시작
daemon-reload : unit 파일들과 systemd 설정 정보를 다시 로드
```

### Unit 간의 의존성
- Unit 파일의 '[Unit]' 영역에 명시적 종속성 설정을 지원.
- 패키지 매니저를 통해 설치한 경우, 관련된 설정이 포함됨

#### Unit 간의 실행 순서 조정
- Before, After 제약을 지정하여 순서를 조정할 수 있음.
- 명시적으로 요청되지 않은 경우 직렬적인 종속성은 없음 -> 병렬적 수행잉 용이하도록 설계됨. 
