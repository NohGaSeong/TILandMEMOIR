# Pod 복제와 배포에 날개달기
## ReplicaSet은 무엇일까?
ReplicaSet은 Pod 복제본을 생성하고 관리함.
- 더 이상 N개의 Pod을 생성하기 위해 생성 명령을 N번 실행할 필요가 없다.
- ReplicaSet 오브젝트를 정의하고 원하는 Pod의 개수를 replicas 속성으로 선언
- 클러스터 관리자 대신 Pod 수가 부족하거나 넘치지 않게 Pod 수를 조절.

## ReplicaSet의 필요성
Pod에 문제가 생겼을 때
- Pod은 즉시 종료되고 클라이언트 요청을 처리할 수 없다(No Self-Healing)
- 클러스터 관리자가 24/7 동안 Pod 상태를 감시하고 정상 복구해야한다.
- N개의 Pod을 실행하고 상태 이상에 대비할 필요가 있음.

## 결함에 내성을 가진 서비스 환경 만들기
'소프트웨어가 내결함성을 가진다' - fault tolerance
- 소프트웨어나 하드웨어 실패가 발생하더라도 소프트웨어가 정상적인 기능을 수행할 수 있어야한다.
- 소프트웨어가 내결함성이 없으면 고객 요구 사항을 만족시킬 수 없다.
- 사람의 개입없이 내결함성을 가진 소프트웨어를 구성하는게 좋지 않을까?


## ReplicaSet의 역할
Pod/노드 상태에 따라 Pod의 수를 조정할 수 있도록 ReplicaSet에게 역할을 위임한다.
- ReplicaSet을 이용해 Pod 복제 및 복구 작업을 자동화
- 클러스터 관리자는 ReplicaSet을 만들어 필요한 Pod의 개수를 쿠버네티스에게 선언한다.
- 쿠버네티스가 ReplcaSet 요청서에 선언된 Replicas를 읽고 그 수만큼 Pod 실행을 보장한다.

## ReplicaSet을 선언해보자
```.yaml
apiVersion: apps/v1
kind:ReplicaSet
metadata:
  name:blue-app-rs
  labels:
    app:blue-app
spec: # 사용자가 원하는 pod의 바람직한 상태
  selector: # Replicaset이 관리해야하는 pod 을 선택하기 위한 label query
  replicas: # 실행하고자 하는 Pod 복제본 개수 선언
  template  # Pod 실행 정보 - Pod Template과 동일(metadata, spec, ... )
```
match lables
```.yaml
spec:
  selector:       # ReplicaSet이 관리할 Pod 집합 선택
    matchLabels:  
      app:blue-app  # Pod label query 작성
    replicas:3  # 유지할 Pod 복제본 수
    template:         # Pod Template 정의
      metadata:
        labels:
          app:blue-app  # ReplicaSet selector에 정의한 label을 포함해야한다.
      spec:
        containers:
        - name : blue-app
          image: blue-app:1.0
```

## ReplicaSet으로 Pod 레플리케이션 설정 방법
- ReplicaSet을 이용해서 Pod 복제본(replicas)를 생성하고 관리한다.
  - 여러 노드에 걸쳐 배포된 Pod UP/DOWN 상태를 감시하고 replicas 수만큼 실행을 보장하낟.
- ReplicaSet의 spec.selector.matchLabels는 Pod template 부분의 spec.template.matadata.labels와 같아야한다.
- spec.replicas를 선언하지 않으면 기본값은 1이다.  
