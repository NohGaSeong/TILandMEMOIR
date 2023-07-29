## Istio?
- Istio는 마이크로서비스 간 데이터 공유를 제어하는 기반을 제공하는 오픈소스 서비스 메쉬 플랫폼임.
- Istio를 모든 로깅 플랫폼, 텔레메트리 또는 정책 시스템으로 통합하도록 지원하는 API가 포함됨.
- Istio는 온프레미스, 클라우드 호스팅, 쿠버네티스 컨테이너, 가상 머신에서 실행되는 서비스 등 다양한 환경에서 구동되도록 설계되었습니다.
- Istio 아키텍처는 데이터 플레인 및 컨트롤 플레인으로 분류됨.
- 데이터 플레인에서는 조직 환경 내에 sidecar 프록시를 배포하여 Istio 지원이 서비스에 추가됨.
- 이 sidecar 프록시는 마이크로서비스와 나란히 위치하며 다른 프록시에서의 요청을 라우팅함.
- 이러한 프록시는 마이크로서비스 간 네트워크 통신을 가로채는 메쉬 네트워크를 형성함.
- 컨트롤 플레인은 프록시를 관리 및 설정하여 트래픽을 라우팅하며, 구성 요소를 설정하여 정책을 실행하고 텔레메트리를 수집함.