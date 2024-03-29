## Amazon VPC란?

### Virtual Private Cloud(VPC)

VPC는 자체 데이터 센터에서 운영하는 기존 네트워크와 아주 유사한 가상 네트워크입니다. VPC를 생성한 후 서브넷을 추가할 수 있습니다.

### 서브넷

서브넷은 VPC의 IP 주소 범위입니다. 서브넷은 단일 가용 영역에 상주해야 합니다. 서브넷을 추가한 후에는 VPC에 AWS 리소스 배포할 수 있습니다.

### IP 주소 지정

VPC 와 서브넷에 IP 주소를 할당할 수 있습니다. 퍼블릭 IP의 GUA 주소를 AWS로 가져오고 VPC의 리소스에 할당 가능함.

### 라우팅

rtb 를 사용하여 서브넷 또는 게이트웨이의 네트워크 트래픽이 전달되는 위치를 결정

### 게이트웨이 및 엔드포인트

게이트웨이는 VPC를 다른 네트워크에 연결, 예를 들면 인터넷 게이트웨이를 사용하여 VPC를 인터넷에 연결함.

VPC 엔드포인트를 사용하여 인터넷 게이트웨이 또는 nat 장치를 사용하지 않고 aws 서비스에 비공개로 연결.

### 피어링 연결

VPC 피어링 연결을 사용하여 두 VPC의 리소스 간 트래픽을 라우팅합니다.

### 트래픽 미러링

중앙 허브 역할을 하는 전송 게이트웨이를 사용하여 VPC, VPN 연결 및 AWS Direct Connect 연결 간에 트래픽을 라우팅합니다.

### VPC 흐름 로그

흐름 로그는 VPC의 네트워크 인터페이스로 들어오고 나가는 ip 트래픽에 대한 정보를 캡쳐합니다.

### VPN 연결

aws virtual private network 을 사용하여 온프레미스 네트워크에 vpc 를 연결합니다.

## Amazon VPC 시작하기

aws 계정에는 기본 vpc aws 리전이 있음. 기본 VPC는 EC2 인스턴스 시작 및 연결을 즉시 시작할 수 있도록 구성되어있음. 

필요한 서브넷. ip주소, 게이트웨이 및 라우팅으로 추가 VPC를 생성하도록 선택할 수 있음.

## Amazon VPC 작업

- Amazon Management Console - VPC 에 액세스할 때 사용할 수 있는 웹 인터페이스를 제공.
- AWS Command Line Interface(AWS CLI) - Amazon VPC를 포함한 다양한 AWS 서비스에서 사용되는 명령을 제공하여 여러 운영체제에서 지원.
- AWS SDK - 언어별 API를 제공, 서명 계산, 요청 재시도 처리 및 오류 처리와 같은 많은 연결 세부 정보를 관리함. 자세한 정보는 AWS SDK 를 참조.
- **쿼리 API** — HTTPS 요청을 사용하여 호출하는 하위 수준의 API 작업을 제공합니다. 쿼리 API 사용이 Amazon VPC에 액세스하는 가장 직접적인 방법이지만, 애플리케이션에서 요청에 서명할 해시 생성 및 오류 처리와 같은 하위 수준의 세부 정보를 처리해야 합니다. 자세한 내용은 *Amazon EC2 API Reference*(Amazon EC2 API 참조)의 [Amazon VPC actions](https://docs.aws.amazon.com/AWSEC2/latest/APIReference/OperationList-query-vpc.html)(Amazon VPC 작업)를 참조하세요.

## Amazon VPC 요금

VPC 사용에 따르는 추가 요금은 없음.

NAT 게이트웨이, IP 주소 관리자, 트래픽 미러링, Reachability Analyzer, Network Access Analyzer과 같은 일부 VPC 구성 요소에 대한 요금이 부과.

# VPC 보안그룹

보안그룹 = 연결된 리소스에 도달하고 나갈 수 있는 인,아웃 바운드 트래픽을 제어함.

VPC를 생성 ⇒ VPC는 기본 보안 그룹과 함께 제공. 각 VPC에 대해 추가 보안 그룹을 생성할 수 있음. 보안 그룹은 해당 보안 그룹이 생성된 VPC의 리소스에만 연결할 수 있음.

## 보안그룹의 기본사항

### 보안그룹의 특징

- 보안 그룹 이름은 VPC 내에서 고유해야함.
- 이름과 설명은 최대 255자일 수 있음.
- 이름과 설명은 다음과 같은 문자가 포함될 수 없음. a-z, A-Z, 0-9, 공백 및 ._-:/()#,@[]+=&;{}!$*
- 이름 끝의 공백이 있으면 그 공백은 잘려나감.
- 보안그룹의 이름은 sg- 로 시작할 수 없음.

상태가 저장이됨. 사용자가 인스턴스에서 요청을 전송하면 해당 요청의 응답 트래픽은 인바운드 보안 그룹 규칙에 관계없이 인스턴스에 도달할 수 있음. 

VPC당 생성할 수 있는 보안 그룹의 개수, 각 보안 그룹에 추가할 수 있는 규칙의 개수, 그리고 네트워크 인터페이스에 연결할 수 있는 보안 그룹의 개수에는 할당량이 있음.

### 보안 그룹 규칙의 특징

- 허용 규칙  ⇒ 지정 가능, 거부 규칙 ⇒ 지정 X
- 보안그룹을 처음 만들때 인바운드 규칙이 없음.
- 보안그룹을 처음 만들때 모든 아웃바운드 트래픽을 허용하는 아웃바운드 규칙이 있음. 특정 아웃바운드 트래픽만 허용하는 아웃바운드 규칙을 추가할 수 있으며, 보안 그룹에 아웃바운드 규칙이 없는 경우 어떤 아웃바운드 트래픽도 허용하지 않음.
- 여러 보안 그룹을 리소스와 연결하면 각 보안 그룹의 규칙이 집계되어 액세스 허용 여부를 결정하는 데 사용되는 단일 규칙 집합을 형성함.
- 규칙 추가, 업데이트 또는 제거할 때 변경 사항은 보안 그룹과 연결된 모든 리소스에 자동으로 적용. 일부 규칙 변경 사항이 미치는 효과는 트래픽의 추적 방법에 따라 다를 수 있음.

**모범사례**

- 특정 IAM 보안 주체에만 보안 그룹을 생성 및 수정하는 권한을 부여
- 오류 위험을 줄이려면 필요한 최소 보안 그룹 수를 생성. 각 보안 그룹을 사용하여 함수 및 보안 요구 사항이 비슷한 리소스에 대한 엑세스 권한을 관리함.
- EC2 인스턴스에 액세스 할 수 있도록 22(SSH) or 3389(RDP) 에 대한 인바운드 규칙을 추가하는 경우 특정 IP 주소 범위만 권한을 부여합니다. 0.0.0.0/0(IPv4)과 ::/(IPv6)를 지정하면 누구든지 지정된 프로토콜을 사용하여 모든 IP 주소에서 인스턴스에 액세스할 수 있게 됩니다.
- 큰 포트범위를 열지마삼, 각 포트를 통한 액세스 권한이 해당 포트를 필요로 하는 원본 또는 대상으로 제한되도록 해야함.
- 보안그룹과 비슷한 규칙으로 네트워크 ACL을 생성하여 VPC에 추가 보안 계층을 추가가능.

## VPC에 대한 기본 보안 그룹

기본 VPC와 사용자가 생성한 VPC는 기본 보안 그룹과 함께 제공함. 일부 리소스의 경우, 리소스를 생성할 때 보안그룹을 연결하지 않을 경우 기본 보안그룹이 연결됨. (EC2 인스턴스가 그 예임)

기본 보안 그룹에 대한 규칙을 변경 가능. 기본 보안 그룹을 삭제할 수 없고, 기본 보안그룹을 삭제하려고하면 `Client.CannotDelete` 오류가 표시됨.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/43049da1-f2e4-44f7-be24-3526b7379cfc/Untitled.png)

## 보안 그룹 규칙

보안그룹의 규칙은 연결된 리소스에 도달,나갈 수 있는 인,아웃 바운드 트래픽을 제어함.

보안 그룹의 규칙을 추가하거나 제거할 수 있음. 규칙은 인바운드 트래픽이나 아웃바운드 트래픽에 적용됨. 특정 CIDR 범위 또는 VPC나 피어 VPC(VPC 피어링 연결 필요)의 다른 보안 그룹에 대한 액세스 권한을 부여할 수 있음.

프로토콜 : 허용할 프로토콜, 가장 일반적인 프로토콜은 6(TCP), 17(UDP), 1(ICMP) 

포트범위 : TCP, UDP 또는 사용자 지정 프로토콜의 경우 허용할 포트의 범위, 단일 포트 번호(예-22) 또는 포트 번호의 범위(예-7000~8000)을 지정할 수 있음.

ICMP 유형 및 코드 : ICMP의 경우, ICMP 유형과 코드. 예를 들어 ICMP 에코 요청에 대해 유형 8을 사용하고 ICMPv6 에코 요청에 대해 유형 128을 입력.

소스 또는 대상 : 허용할 트래픽에 대한 소스(인바운드 규칙) 또는 대상(아웃바운드 규칙), 다음 중 하나를 지정하자.

- 단일 IPv4 주소. /32 접두사 길이
- 단일 IPv6주소. /128 접두사 길이
- CIDR 블록 표기법으로 표시된 IPv4 주소의 범위
- CIDR 블록 표기법으로 표시된 IPv6 주소의 범위
- 접두사 목록의 ID
- 보안그룹의 ID

# VPC 흐름 로그를 사용하여 IP 트래픽 로깅

vpc 흐름 로그는 VPC의 네트워크 인터페이스에서 전송되고 수신되는 ip 트래픽에 대한 정보를 수집할 수 있는 기능. 흐름 로그 데이터는 Amazon Cloudwatch logs, amazon s3 또는 amazon kinesis date firehose에 게시될 수 있다. 흐름 로그를 생성하면 구성한 로그 그룹, 버킷 또는 전송 스트림의 흐름 로그 레코드를 검색하고 볼 수 있음.

흐름 로그는 다음과 같은 여러 작업에 도움이 될 수 있음.

- 지나치게 제한적인 보안 그룹 규칙 진단
- 인스턴스에 도달하는 트래픽 모니터링
- 네트워크 인터페이스를 오가는 트래픽 방향 결정

흐름 로그 데이터는 네트워크 트래픽 경로 외부에서 수집되므로 네트워크 처리량이나 지연 시간에 영향을 주지 않는다. 네트워크 성능에 영향을 주지 않고 흐름 로그를 생성하거나 삭제할 수 있음. 

## 흐름 로그 기본 사항

VPC, 서브넷 또는 네트워크 인터페이스에 대한 흐름 로그를 생성할 수 있음. 서브넷이나 VPC에 대한 흐름로그를 생성할 경우, VPC또는 서브넷 각 네트워크 인터페이스가 모니터링됨.

모니터링된 네트워크 인터페이스를 위한 흐름 로그 데이터는 트래픽 흐름을 설명하는 필드로 구성된 로그 이벤트인 흐름 로그 레코드(flow log record)로 기록됨.

흐름 로그를 생성하려면 다음을 지정해야함.

- 흐름 로그를 생성할 리소스
- 캡처할 트래픽 유형(허용된 트래픽, 거부된 트래픽 또는 모든 트래픽)
- 흐름 로그 데이터를 게시할 대상
    
    

흐름 로그를 생성한 후에, 데이터를 수집하여 선택된 대상에 게시하는데 몇 분의 시간이 소요될 수 있음. 흐름 로그는 네트워크 인터페이스에 대한 로그 스트림을 실시간으로 캡처하지 않음

서브넷이나 VPC에 대한 흐름 로그를 생성한 후 서브넷에서 하나의 인스턴스를 시작할 경우, 해당 네트워크 인터페이스에 대한 네트워크 트래픽이 생기는 즉시 새로운 네트워크 인터페이스에 대한(CloudWatch Logs용)로그 스트림 또는 (Amazon S3) 로그 파일 객체가 생성됨.

다음과 같은 다른 AWS 서비스에서 생성한 네트워크 인터페이스에 대한 흐름 로그를 생성할 수 있습니다.

- Elastic Load Balancing
- Amazon RDS
- Amazon ElastiCache
- Amazon Redshift
- Amazon WorkSpaces
- NAT 게이트웨이
- 전송 게이트웨이

네트워크 인터페이스 유형에 관게없이 Amazon EC2 콘솔 또는 Amazon EC2 API 를 사용하여 네트워크 인터페이스에 대한 흐름 로그를 작성해야함.

흐름 로그에 태그를 적용할 수 있음. 각 태그는 사용자가 정의하는 키와 선택적 값으로 구성됨. 태긎는 흐름 로그를 용도나 소유자별로 구성하는 데 도움이 될 수 있음.

흐름 로그가 더 이상 필요하지 않을 경우 삭제할 수 있음. 흐름 로그를 삭제하면 리소스에 대한 흐름 로그 서비스가 비활성화 되어 생서되거나 게시되는 새 흐름 로그 레코드가 없음. 흐름 로그를 삭제해도 기존ㅇ 흐름 로그 데이터는 삭제되지 않음. 흐름 로그를 삭제하면 작업을 마무리했을 때 대상에서 직접 흐름 로그 데이터를 삭제할 수 있습니다.

## 흐름 로그 레코드

흐름 로그 레코드는 VPC에 네트워크 흐름을 나타냄. 기본적으로 각 레코드는 캡처 기간이라고도 하는 집계 간격 내에 발생하는 네트워크 인터넷 프로토콜 트래픽 흐름을 캡처

각 레코드는 필드가 공백으로 구분되어 있는 문자열. 레코드에는 소스, 대상, 프로토콜 등 IP 흐름의 다양한 구성 요소에 대한 값이 포함.

흐름 로그를 생성할 때 흐름 로그 레코드의 기본 형식을 사용하거나 사용자 지정 형식을 지정할 수 있음.

### 집계 간격

특정 흐름이 캡처되어 흐름 로그 레코드로 집계되는 기간. 기본적으로 최대 집계 간격은 10분. 흐름 로그를 만들 때 선택적으로 최대 집계 간격을 1분으로 지정. 최대 집계 간격이 1분인 흐름 로그는 최대 집계 간격이 10분인 흐름 로그보다 더 많은 양의 흐름 로그 레코드를 생성

네트워크 인터페이스가 NITRO 기반 인스턴스에 연결된 경우 집계 간격은 지정된 최대 집계 간격에 관계없이 항상 1분 이하.

집계 간격 내에서 데이터를 캡처, 데이터 처리, cloud watch logs OR amazon s3 에 게시하느라 추가 시간이 걸림. 흐름 로그 서비스는 일반적으로 로그를 약 5분만에 cloudwatch logs 로 전송하고 약 10분만에 amazon s3로 전송합니다. 

### 기본 형식

기본 형식의 흐름 로그 레코드에는 사용 가능한 필드 테이블에 표시되는 순서대로 버전 2 필드가 포함됨. 기본 형식을 사용자 정의하거나 변경할 수 없음. 추가 필드 또는 다른 필드 하위 세트를 캡처하려면 사용자 지정 형식을 정함.

### 사용자 지정 형식

사용자 지정 형식을 사용하면 흐름 로그 레코드에 포함되는 필드와 그 순서를 지정할 수 있음. 이를 통해 요구 사항에 맞는 흐름 로그를 만들고 관련이 없는 필드를 생략 가능. 사용자 지정 형식을 사용하면 게시된 흐름 로그에서 특정 정보를 추출하기 위해 별도의 프로세스가 필요하지 않음. 사용 가능한 흐름 로그 필드를 얼마든지 지정할 수 있지만 하나 이상을 지정해햐한다.

## 흐름 로그 요금

흐름 로그를 게시하면 벤딩 로그에 대한 데이터 모으기 및 보관 요금이 적용됩니다. 

# VPC 피어링이란?

VPC는 사용자의 AWS 계정 전용 가상 네트워크입니다. VPC는 AWS 클라우드에서 다른 가상 네트워크와 논리적으로 분리되어 있습니다. AWS 리소스(예: EC2 인스턴스)를 VPC에서 시작할 수 있습니다.

VPC 피어링 연결은 프라이빗 IPv4 주소 또는 IPv6 주소를 사용하여 두 VPC 간에 트래픽을 라우팅할 수 있도록 하기 위한 두 VPC 사이의 네트워킹 연결입니다. 동일한 네트워크에 속하는 경우와 같이 VPC의 인스턴스가 서로 통신할 수 있습니다. 사용자의 자체 VPC 또는 다른 AWS 계정의 VPC와 VPC 피어링 연결을 만들 수 있습니다. VPC는 상이한 리전에 있을 수 있습니다(리전 간 VPC 피어링 연결이라고도 함).

AWS는 VPC의 기존 인프라를 사용하여 VPC 피어링 연결을 생성합니다. 이는 게이트웨이도, VPN 연결도 아니며 물리적 하드웨어 각각에 의존하지 않습니다. 그러므로 통신 또는 대역폭 병목에 대한 단일 지점 장애가 없습니다.

VPC 피어링 연결은 원활한 데이터 전송에 도움이 됩니다. 예를 들어, AWS 계정이 두 개 이상인 경우 이들 계정을 대상으로 VPC를 피어링하여 파일 공유 네트워크를 만들 수 있습니다. VPC 피어링 연결을 사용하여 다른 VPC가 사용자의 VPC 중 하나에 있는 리소스에 액세스하도록 허용할 수도 있습니다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d86b0bcc-cc48-41bf-b1fc-a977bde369e8/Untitled.png)

서로 다른 AWS 리전에 위치한 VPC 사이에 피어링 관계를 설정하는 경우 상이한 AWS 리전의 VPC에 있는 리소스(예: EC2 인스턴스와 Lambda 함수)에서 게이트웨이, VPN 연결 또는 네트워크 어플라이언스를 사용하지 않고 프라이빗 IP 주소를 사용하여 서로 통신할 수 있습니다. 트래픽은 프라이빗 IP 공간 안에서 유지됩니다. 모든 리전 간 트래픽은 암호화되며 단일 장애 지점 또는 대역폭 제한이 없습니다. 트래픽은 항상 글로벌 AWS 백본에서만 유지되고 절대로 퍼블릭 인터넷을 통과하지 않으므로 일반적인 취약점 공격과 DDoS 공격 같은 위협이 감소합니다. 리전 간 VPC 피어링은 리전 간에 리소스를 공유하거나 지리적 중복성을 위해 데이터를 복제할 수 있는 간단하고 비용 효율적인 방법을 제공합니다.

## **VPC 피어링 연결 요금**

VPC 피어링 연결 생성에는 요금이 부과되지 않지만 피어링 연결을 통한 데이터 전송에는 요금이 부과된다.
