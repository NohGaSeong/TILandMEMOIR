## 운영환경에서 Pod의 한계점
### 변경이 잦은 Pod Ip 목록에 영향을 받는 파드 클라이언트
- 파드 클라이언트가 최신 상태의 모든 Pod IP를 알고 있어야함.
- 클라이언트가 특정 Pod Ip로 오프라인 상태의 Pod에 접근했따면 요청을 실패함.

### Pod IP는 클러스터 내부에서만 접근 가능
- 클러스터 외부에서 접근할 수 있는 방법이 필요함.
- kubectl port-forward 프로세스는 개발 단계에서만 사용해야함. (장고 등과 마찬가지로 안정성과 보안 문제인듯 싶음)

## Service 개념과 특징, 활용 방법
### Service: 파드 추상화 = 파드들의 단일 엔드포인트 + 로드밸런싱
- 파드 클라이언트는 Service IP:Port를 이용해서 파드와 통신할 수 있다.
- Service는 Selector에 의해 선택된 파드 집합 중 임의의 파드로 트래픽을 전달한다.

### EndPoints: Service가 노출하는 Pod IP와 Port의 최신 목록
- Service 리소스를 생성하면 Service와 같은 이름으로 Endpoints 리소스가 생성된다.
- Service에 선언한 Selector의 파드 집합이 변경될 때마다 Endpoints 목록도 업데이트됨.
- Service가 받은 트래픽을 Endpoints 중에 하나로 리다이렉트한다.

## Service로 통신하기
### A. 환경변수를 이용하는 방법
- 쿠버네티스가 Pod을 생성할 때 컨테이너 환경변수에 모든 Service IP와 Port를 추가한다.
- OOO_SERVICE_HOST, OOO_SERVICE_PORT
- 주의 1. Service를 클라이언트 Pod보다 먼저 생성해야 한다.
- 주의 2. 다른 네임스페이스에 있는 Service 환경변수는 설정되지 않는다.

### B. DNS 서버를 이용하는 방법
- 쿠버네티스가 DNS 서버 IP 주소를 컨테이너의 /etc/resolve.conf 파일에 등록
- Service 이름으로 요청을 실행하면 DNS 서버로부터 Service IP를 조회할 수 있음.

## Pod을 외부로 노출하는 다양한 Service 타입
### ClusterIP , NodePort, LoadBalancer 타입
- Service 타입에 따라 클라이언트가 Service에 접근할 수 있는 방식이 달라짐.
- LoadBalancer 타입은 NodePort, ClusterIP 기능을 모두 포함한다.

### ClusterIP 타입
- 기본 Service 타입, Pod IP처럼 외부에서는 접근할 수 없는 IP를 할당받는다.
- 이 때 Service IP는 클러스터 내부 통신용으로 사용된다.

### NodePort 타입
- 외부에서 접근할 수 있는 External IP가 아니라 NodePort를 할당 받는다.
- 할당받은 노드 Port를 통해 들어온 트래픽을 파드 집합으로 포워딩한다.
#### 한계점
- 지정한 노드가 사용할 수 없는 상태라면?
- 로드밸런서를 이용해서 건강한 상태의 노드로 트래픽을 전달할 수 있도록 만든다.
### LoadBalancer 타입
- 클라우드 서비스의 Load Balancer를 프로비저닝하고 External IP를 할당 받는다.
- 클라이언트는 Load Balancer IP를 통해 특정 서비스로 외부 트래픽을 포워딩할 수 있다.

## 요약
- Serivce 리소스는 파드 집합에 대한 단일 엔드포인트를 제공함.
- ClusterIp Service를 이용해서 클러스터 내부 Pod간 통신에 단일 엔드포인트를 만들 수 있음.
- NodePort/LoadBalancer Service를 이용해서 클러스터 외부 트래픽을 Pod으로 전달할 수 있음.
- Pod 안에서는 Service 이름과 네임스페이스 이름을 이용해서 다른 Pod과 통신할 수 있다.
  - 같은 네임스페이스에 있는 Pod:<service-name>:<service-port>
  - 다른 네임스페이스에 있는 Pod:<service-name>:<service-port><namespace>
