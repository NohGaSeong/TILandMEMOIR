## Ingee를 통해 Service를 외부로 노출하는 방법
### 왜 필요할까?
- 수많은 로드밸런서의 IP를 기억해야하는 클라이언트 부담. (Service의 수만큼의 Public IP를 기억해야함)

### Ingress: Service 추상화, 의미있는 단일 엔드포인트 제공
- 트래픽을 Service로 분산하기 위한 라우팅 규칙 모음
- 클라이언트가 호출한 Host 헤더나 path를 통해 Service를 구분하고 트래픽을 포워딩

### Ingress Controller: Ingress 규칙에 따라 트래픽 분산을 실행하기 위한 리소스
- 쿠버네티스 클러스터 제공자가 구현한 ingress controller마다 기능이 다르다
- 쿠버네티스 지원 ingress controller를 찾아보는 사이트가 있다.

## 특징
- 클라이언트는 클러스터 안에 있는 여러 Service를 하나의 Ip로 접근할 수 있음.
- 쿠버네티스 클러스터에 존재하는 Service 리소스에 대한 라우팅 규칙을 선언한다.
- Ingress Controller가 받은 HTTP Requeset 의 host 헤더 정보나 URL path에 따라 여러 서비스로 트래픽을 분산할 수 있다.
