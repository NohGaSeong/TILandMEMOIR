# Pod 소개
## Pod 의 개념과 특징
### Pod은 여러 컨테이너를 감싸고 있는 콩껍질과 같다.
- 노드에서 컨테이너를 실행하기 위한 가장 기본적인 배포 단위
- 여러 노드에서 1개 이상의 pod 을 분산 배포/실행 가능(pod replicas)

### 쿠버네티스가 생성하는 pod 은 이런 특징이 있음.
- 쿠버네티스는 pod을 생성할 때 노드에서 유일한 Ip를 할당(서버 분리 효과)
- pod 내부 컨테이너 간에 localhost로 통신 가능, 포트 충돌 주의!
- pod 안에서 네트워크와 볼륨 등 자원을 공유

## Pod 네트워킹 : Pod IP
### PodIP는 클러스터 안에서만 접근할 수 있다.
- 클러스터 외부 트래픽을 받기 위해서는 Service 혹은 Ingress 오브젝트가 필요.

## Pod 단위 배포와 스케일 아웃
### 단 하나의 명령어로 원하는 수만큼 Pod 생성
`$ kubectl scale deployment orderapp --replicas=3`
deployment.apps/orderapp scaled

`$ kubectl get pod` 등등

### pod 과 컨테이너 설계 시 고려할 점
1. 컨테이너들의 라이프 사이클이 같은가?
  - Pod 라이프사이클 = 컨테이너들의 라이프 사이클
  - 컨테이너 A가 종료되었을때 컨테이너 B 실행이 의미가 있는가
2. 스케일링 요구사항이 같은가?
  - 웹 서버 vs 데이터베이스, 트래픽이 많은 vs 그렇지 않은
3. 인프라 활용도가 더 높아지는 방향으로
  - 쿠버네티스가 노드 리소스 등 여러 상태를 고려하여 Pod을 스케쥴링 

## Pod 배포
### 노드에 배포되는 과정
1. 사용자로부터 Pod 배포 요청을 수락한다.
2. 요청 받은 수 만큼 Pod Replica를 생성한다.
3. Pod을 배포할 적절한 노드를 선택한다.
4. 5에게 이미지 다운로드를 명령하고 Pod 실행을 준비한다. Pod 상태를 업데이트한다.
5. 이미지를 다운로드하고 컨테이너를 실행한다.

## Pod 오브젝트 표현 방법
### 기본 속성
```.yaml
apiVersion: v1 # Kubernetes API 버전
kind: pod      # 오브젝트 타입
metadata:      # 오브젝트를 유일하게 식별하기 위한 정보
  name:kube-basic   # 오브젝트 이름
  labels:           # 오브젝트 집합을 구할때 사용할 이름표
    app:kube-basic
    project:fastcampus
    
spec:            # 사용자가 원하는 오브젝트의 바람직한 상태
  nodeSelector:  # Pod을 배포할 노드
  containers:    # Pod 안에서 실행할 컨테이너 목록
  columes:       # 컨테이너가 사용할 수 있는 볼륨 목록
```

### spec.nodeSelector 속성 - 노드 선택
```.yaml
spec:
  nodeSelector: # Pod 배포를 위한 노드를 선택
    gpu: "true" # 노드 집합을 구하기 위한 식별자(key:value)
```
### spec.nodeSelector 속성 - 컨테이너 정보
```.yaml
sepc:
  containers:
  - name : kube-basic   # 컨테이너 이름
  image: kube-basic:1.0   # 도커 이미지 주소
  imagePullPolicy: "Always" # 도커 이미지 다운로드 정책
  ports:
    - containerPort:80     # 통신에 사용할 컨테이너 포트
```

```yaml
sepc:
  containers:
  -name:kube-basic
  image:kube-basic:1.0
  
  env:                  # 컨테이너에 설정할 환경변수 목록
    - name: PROFILE     # 환경변수 이름
    value : production  # 환경변수 값
    - name: MESSAGE
    value : this application is running on $(PROFILE)   # 다른 환경변수 참조
```

```yaml
spec:
  containers:
  -name:kube-basic
  image:kube-basic:1.0
  valumeMounts:         # 컨테이너에서 사용할 pod 볼륨 목록
  - name : html         # pod 목록 이름
  mountPath: /var/html  # 마운트할 컨테이너 경로
  -name: web-server
  image : nginx
  volumeMounts:
  - name : html
  mountPath: /usrshare/nginx/html #같은 pod 볼륨을 다른 경로로 마운트
```
```.yaml
spec:
  containers:
  volumes:            # 컨테이너가 사용할 수 있는 볼륨 목록
  - name : host-volume  # 볼륨 이름
  hostPath:           # 볼륨 타입, 노드에 있는 파일이나 디렉토리를 마운트하고자 할 때
    path: /data/mysql
```

## Pod의 한계점
1. Pod이 나도 모르는 사이에 종료되었다면?
- 자가 치유능력이 없음. pod이나 노드 이상으로 종료되면 끝
- 사용자가 선언한 수만큼 pod 을 유지 해주는 replicaset 오브젝트 도입

2. pod ip는 외부에서 접근할 수 없다, 그리고 생성할 때마다 ip가 변경된다.
- 클러스터 외부에서 접근할 수 있는 고정적인 단일 엔드포인트 필요
- Pod 집합을 클러스터 이부로 노출하기 위한 Service 오브젝트 필요.

### Pod 생성과 배포
- Pod은 여러 개의 컨테이너를 포함할 수 있고 하나의 노드에 배포된다.
- Pod을 YAML 파일로 정의 해두면 필요할 때 원하는 수 만큼 노드에 배포할 수 있다.
- Pod과 컨테이너를 1:1로 기본 설계하고 특별한 사유가 있는 경우 1:N 구조를 고민한다.

### Pod IP
- 쿠버네티스는 Pod을 생성할 때 클러스터 내부에서만 접근할 수 있는 Ip 를 할당한다.
- Pod IP는 컨테이너와 공유되기 때문에 컨테이너 간 포트 충돌을 주의해야한다.
- 하나의 Pod에 속한 컨테이너들은 localhost로 통신할 수 있따.
- 다른 Pod(컨테이너)과 통신은 Pod IP를 이용한다. 
