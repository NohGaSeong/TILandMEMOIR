# VPC?
- aws private 격리된 프라이빗 섹션
- 배포하고 사용자가 지정할 수 있는 가상 네트워크 토폴로지
- 자체 데이터센터의 네트워크와 유사
- 모든 Account는 기본적으로 vpc가 생성됨

## customer benefits

control network architecture
- 네트워크 아키텍처를 제어하는 IP 범위
- 비밀 서브넷, 공용 서브넷
- 네트워크 게이트웨잉
- 보안설정 구성
- 토폴로지의 유연성
- VPC 피어링
- IPv6의 지원

Evolving EC2 feature set
- 고정 사설 IP 주소 할당
- EC2 기반 고정된 public ip 를 사용 가능
- 인스턴스에 여러 NIC 및 ip를 할당할 수 있음

Improve security & compliance posture
- 하나의 aws 계정에만 논리적으로 격리된 vpc 아웃바운드 트래픽에 대한 송신 필터링
- 인스턴스는 기본적으로 인터넷에 액세스할 수 없음
- 단일 테넌트 하드웨어에서 인스턴스 실행
- 개발 , 테스트 및 프로덕션을 위한 격리
- VPC EndPoint를 통해 인터넷 연결이 안되더라도 AWS 서비스에 비공개 접근이 가능

Enables Hybrid Cloud Architectures
- on premise 네트워크를 aws cloud로 확장
- ipsec vpn 에 대한 지원
- vpc dx에 대한 연결

## perfromance
향상된 네트워킹 
  
## Security
Network level controls
- 프라이빗 amazon s3엔드포인트
- 프라이빗 dynamodhb 엔드포인트
- private link 를 통해 18개 이상 서비스 연결 가능
* privateLink는 amazon vpc에서 비공개 서비스 접근이 가능합니다. 각 private link는 할당된 서브넷의 사설 ip로 표시 가능합니다.

## Access
Access options
- vpc peering을 통해 여러 vpc에 대한 보안연결이 가능해요
- AWS Transit Gateway를 사용하면 고객이 vpc와 on-premise 환경 각 단일 GW를 연결할 수 있습니다.

### Access options
- VPC에 대한 AWS DirectConnect Private 연결

## Roution Table
- 각 서브넷은 연결된 라우팅 테이블이 있습니다
- 라우팅 테이블은 여러 서브넷과 연결될 수 있습니다.

## Routing
- 라우팅 테이블은 다음으로 보내집니다.
- 
- 서브넷은 인터넷 게이트웨이에 대한 경로가 있는 경우 "공용 서브넷 이라고 합니다"
- 수평 확장, 중복, 고가용성 구성요소
- VPC 서브넷을 인터넷에 연결
- 라우팅 테이블에서 참조 가능
- 공용 및 사설 IP 주소 간의 1:1 NAT 수행

## Public IP addressing : Elastic IP Address
- AWS Account 와 연결된 정적 publicIP 주소
- 동적으로 할당됨
- 인스턴스 또는 네트워크 인터페이스와 연결 가능

## Outbound only traffic : nat gateway
- 인터넷에 대한 아웃바운드 연결활성화
- aws 에서 완벽한 고가용성을 가져간다
- 네트워크 ACL은 NAT 게이트웨이 트래픽에 적요ㅕㅇ된다
- TCP,UDP,ICMP 프로토콜 지원

## IP FW : Network Access Control list
- 인바운드 아웃바운드 검사
- 선택적 보안 수준
- 기본 모든 트래픽 허용
- IP 및 TPC/UDP 포트 지원

## Resource FW: security group
- 상태 저장 방화벽
- 인바운드 아웃바운드 고객 정의 규칙
- 인스턴스 인터페이스 수준 검사

등

## Network ACLs vs securityy group
NACLs : 서브넷에 적요ㅕㅇ됨, 상태 비 추적, 허용 및 거부, 순서대로 처리되는 규칙
Security group : 인스턴스 ENI당 최대 5개, 상태 저장 추적, Allow 기반 필터링

## Connect multiple vpcs : vpc peering
- 확장성 및 고가용성
- aws account 간 지원
- aws 전체 region에서 지원
- 양방향ㅌ ㅡ래픽
- 원격 보안 그룹 참조 가능
- 라우팅 테이블 사용한 라우팅 정책
- 모든 서브넷이 서로 연결할 필요는 없음
- 겹치는 IP 주소가 없어야함

### use vpc peering to connect vpc
- 동일한 리전내의 vpc 동일 ip에 대한 접근은 불가
- 다른 account ip 대역은 겹칠 수 없다
- 두 vpc사이에 하나만 다른 리전에서 vpc간 피어링이 가능하다



