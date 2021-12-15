# (VPC) AWS 네트워킹의 동작원리
## vpc?
- 가상의 프라이빗 클라우드를 이용하여 사용자가 정의한 `가상 네트워크`로 aws 리소스를 시작할 수 있습니다.
- 이 가상 네트어크는 aws의 확장 가느한 인프라를 사용한다는 이점과 함께 고객의 자체 데이터 센터에서 운영하는 `기존 네트워크와 매우 유사`합니다
## VPC의 특징
- 계정 생성 시 default로 vpc를 만들어 줌
- Ec2, rds,s3 등의 서비스 활용 가능
- 서브넷 구성
- 보안설정(ip block, inbound outbound 설정)
- vpc peering(vpc 간의 연결)
- ip 대역 지정 가능
- vpc는 하나의 region 에만 속할 수 있음(다른 region으로 확장 불가능)
## components of vpc
![image](https://user-images.githubusercontent.com/82383294/146148591-121649b4-9f9f-4599-8bfc-2d45f39e911e.png)
## VPC의 구성요소
### Availability Zone
- 물리적으로 분리되어 있는 인프라가 모여 있는 데이터 센터
- 각 AZ는 일정 거리 이상 떨어져 있음
- 하나의 리전은 2개 이상의 AZ로 구성됨
- 각 계정의 AZ는 다른 계정의 AZ와 다른 아이디를 부여받음.
### Subnet(CIDR)
- vpc의 하위 단위(sub + network)
- 하나의 az에서만 생성 가능
- 하나의 az에는 여러개의 subnet 생성 가능
- 크게 2가지의 서브넷으로 나뉜다
  - Private subnet : 인터넷에 접근 불가능한 subnet
  - Public subnet : 인터넷과 소통 가능한 subnet
- CIDR 블록을 통해 서브넷을 구분(저번에 배운 네트워크 개요 참조)
- `Region` 안에 `VPC` 안에 `AZ` 안에 `Subnet`이 존재합니다.
- 
### Internet GateWay 
- 인터넷으로 나가는 통로
- Private subnet은 IGW로 가지 않는다. (연결 안돼있다? 라기 보단 가지 않는게 맞는듯)
  - why ? : 외부 인터넷과 소통이 불가능하기 떄문에 
![image](https://user-images.githubusercontent.com/82383294/146173024-a327d1ec-97f3-4bc8-a37d-5e24b0200f3d.png)
### Network Access Control List/secuiry group
- 보안 검문서
- NACL -> Stateless, SG -> Stateful
- Access Block 은 NACL 에서만 가능
![image](https://user-images.githubusercontent.com/82383294/146174282-7337bec7-e997-4997-a074-179eab7268a3.png)

### Route Table
- 트래픽이 어디로 가야 할지 알려주는 테이블
- VPC 생성 시 자동으로 만들어줌
  - 10.0.0.0/16(10.0.0.0 ~ 10.0.255.255까지) -> Local
  - 나머지는 IGW
 - 10.0.0.0/16 => Target = Local
 - 0.0.0.0/0 => Target = IGW-ID
 - ::/0 => Target = IGW-ID 
 - 여기서 0.0.0.0/0 과 ::/0 이 없다면 10.0.0.0/16 이 들어오면 local로 잘 접근이 되는데 다른 ip가 들어오면 갈 데가 없음
 
### NAT(Network Address Translation)instance/NAT gateway
- private는 주로 데이터베이스 등 보안적으로 중요한것들을 private subnet에 담아둡니다.
- 프라이빗에서 퍼블릭으로 트래픽을 쏘고 퍼블릭에서 인터넷게이트웨이로 트래픽을 쏘는겁니다. (하나의 vpc 안에 있기때문에 통신 가능) 
- 위와 같은 우회를 NAT GATEWAY 가 도와줍니다.
- private 서브넷 안에 있는 ec2 가 public 서브넷 안에 있는 nat gateway 와 nat instance 로 연결해 이 public 서브넷 안에 있는 요소들이 인터넷과 연결해줍니다.
- 
### VPC endpoint

