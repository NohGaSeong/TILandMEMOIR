# Deployment 소개
## Replicaset을 이용해 pod을 배포함. 왜?
- ReplicaSet의 Pod 복제 기능을 이용해 여러개의 Pod을 한 번에 실행할 수 있음.
- 선언한 replicas 수만큼 pod 실행을 보장함.
- Replicaset이 우리 대신 pod 상태를 감시함.
- Pod 실행 중에도 replicas 조정이 자유롭다.

## Replicaset을 이용한 배포 과정
1. Replicaset - pod 1.0 배포 명령을 내리면
2. Replicaset - pod template 이미지를 2.0으로 변경하고 적용하면
3. Replicaset - 실행 중인 모든 pod 1.0을 삭제하는 명령을 내리면 2.0 버전으로 배포가됨. (롤아웃)
### 4. 돌발상황, 배포한 새로운 pod 에 문제가 있음. 이전 버전으로 롤백 시도.
- 새로운 replicaset을 만들어 pod 재배포 or pod template 변경 후 적용
- 필요없는 replicaset과 pod을 제거
- <b>롤백 혹은 새로운 버전을 배포할 때 마다 1~3번의 과정을 반복</b>
- 반복 작업을 쿠버네티스에게 위임할 수는 없을까?

## 배포 아이디어
### Pod 배포를 위한 3가지 정보
1. selector : 어떤 pod 집합을 대상으로 replication 해야하는지
2. replicas: 얼마나 pod 을 생성할지
3. pod template image: pod 에서 어떤 컨테이너를 실행할지

### 배포할때 바뀌는 버전은 정해져있기에
pod template 이미지가 바뀔때마다 쿠버네티스가 알아서 replicaset을 생성하고 이전 Pod 을 제거해주면 안될까? 라는 의문을 품게됨.

## Deployment란?
### Deployment는 Pod 배포 자동화를 위한 오브젝트 (Replicaset + 배포 전략)
- 새로운 pod을 롤아웃/롤백할 때 replicaset 생성을 대신해줌. (POd 복제)
- 다양한 배포 전략을 제공하고 이전 파드에서 새로운 파드로의 전환 속도를 제어할 수 있음.
- 이제는 Pod을 배포할 때 Replicaset이 아닌 Deployment를 사용함.


## Recreate 과 RollingUpdate 비교
### Recreate
- 새로운 버전을 배포하기 전에 이전 버전이 즉시 종료됨.
- 컨테이너가 정상적으로 시작되기 전까지 서비스하지 못함
- replicas 수만큼의 컴퓨팅 리소스 필요
- 개발 단계에서 유용

### RollingUpdate
- 새로운 버전을 배포하면서 이전 버전을 종료
- 서비스 다운 타임 최소화
- 동시에 실행되는 pod의 개수가 replicas를 넘게 되므로 컴퓨팅 리소스 더 많이 필요

## RollingUpdate 속도 제어 옵션
### maxUnavailable
- 롤링 업데이트를 수행하는 동안 유지하고자 하는 최소 pod의 비율을 지정할 수 있다.
- 최소 pod 유지 비율 = 100 - maxUnavailable 값
- 예 ) replicas:10, maxUnavailable:30%
  - 이전 버전의 pod 을 replicas 수의 최대 30%까지 즉시 scale down 할 수 있다.
  - replicas를 10으로 선언했을 때, 이전 버전의 pod을 3개까지 즉시 종료할 수 있따.
  - 새로운 버전의 pod 생성과 이전 버전의 pod 종료를 진행하면서 replicas 수의 70% 이상의 pod을 항상 running 상태로 유지해야한다.

### maxSurge
- 롤링 업데이트를 수행하는 동안 허용할 수 있는 최대 Pod의 비율을 지정할 수 있다.
- 최대 Pod 허용 비율 = maxSurge 값
- 예 ) replicas:10, maxSurge: 30 %
  - 새로운 버전의 pod을 replicas 수의 최대 30%까지 즉시 scale up 할 수 있다.
  - 새로운 버전의 pod을 3개까지 즉시 생성할 수 있다.
  - 새로운 버전의 pod 생성과 이전 버전의 pod 종료를 진행하면서 총 pod의 수가 replicas 수의 130% 를 넘지 않도록 유지해야한다.

## Revision
- Deployment는 롤아웃 히스토리를 Revision # 으로 관리한다.
- Revision # 를 이용하여 손 쉽게 롤백이 가능하다.
