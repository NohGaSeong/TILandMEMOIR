# Replicaset
## 왜 쓸까?
- Pod을 단독으로 사용하면 Pod에 문제가 생겼을때 자동복구등이 안됨.
- 그래서 이러한 Pod을 정해진 수만큼 복제하고 관리하는 것이 Replicaset

## Replicaset의 명령어와 여러 과정을 알아보자
- 우선 아래와 같은 yml 파일을 만들고
```.yml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: echo-rs
spec:
  replicas: 1
  selector:
    matchLabels:
      app: echo
      tier: app
  template:
    metadata:
      labels:
        app: echo
        tier: app
    spec:
      containers:
        - name: echo
          image: ghcr.io/subicura/echo:v1
```

- 생성 : `kubectl apply -f echo -rs.yml` 로 위의 yml 을 참고해서 replicaset 을 만들어줍니다.
- 확인 : `kubectl get po,rs`
- 위의 명령어들을 입력하면 Replicaset이랑 pod이 같이 생성된 것들을 볼 수 있음.
- spec.selector : label 체크 조건
- spec.replicas : 원하는 Pod의 개수
- spec.template : 생성할 Pod의 명세

### 라벨을 제거하거나 생성하면 어떻게 될까?
- 라벨 제거 : `kubectl label pod/echo-rs-tcdwj app-`(app- 를 지정하면 app label을 제거)
- 다시 Pod 확인 : `kubectl get pod --show-labels`
- 기존에 생성된 Pod의 app label이 사라지면서 selector에 정의한 app=echo,tier=app 조건을 만족하는 Pod의 개수가 0이 되어 새로운 Pod이 만들어졌습니다.
- 다시 app label을 추가해봅니다.
- kubectl label pod/echo-rs-tcdwj app=echo
- replicas에 정의한 대로 Pod의 개수를 1로 유지하기 위해 기존 Pod을 제거합니다.

## ReplicaSet이 어떻게 동작할까?
1. ReplicaSet Controller는 ReplicaSet조건을 감시하면서 현재 상태와 원하는 상태가 다른 것을 체크
2. ReplicaSet Controller가 원하는 상태가 되도록 Pod을 생성하거나 제거
3. Scheduler는 API서버를 감시하면서 할당되지 않은unassigned Pod이 있는지 체크
4. Scheduler는 할당되지 않은 새로운 Pod을 감지하고 적절한 노드node에 배치
5. 이후 노드는 기존대로 동작

- ReplicaSet은 ReplicaSet Controller가 관리하고 Pod의 할당은 여전히 Scheduler가 관리합니다

## Pod을 쉽게 복제해보자
```.yml
spec:
  replicas: 4
```
- 같은 스크립트를 통해 손쉽게 pod을 여러개로 복사할 수 있습니다.
- 위의 스크립트를 따르면 pod이 총 4개로 복제됩니다. (1개가 기존에 있었다면 +3)
## 마치며
- ReplicaSet은 원하는 개수의 Pod을 유지하는 역할을 합니다.
- label을 이용하여 Pod을 체크합니다 (label이 겹치지지 않게 주의해서 정의해야함)
- 실전에서 Replicaset을 단독으로 쓰는 경우는 거의 없습니다. Deployment가 Replicaset을 이용하기 떄문에 주로 Deployment를 이용합니다.
