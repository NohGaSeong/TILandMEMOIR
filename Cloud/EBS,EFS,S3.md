# EBS, EFS, S3. 어떤 스토리지를 써야할까?
## EBS(Elastic Block Storage)
- AWS EC2 (Elastic Compute Cloud)에서 사용하도록 설게된 사용하기 쉬운 고성능 블록 스토리지 서비스
- 가용 영역내에서 복제를 통해 재해복구
- 볼륨의 특정 시점 스냅샷을 S3에 저장할 수 있다
- 마지막 스냅샷 이후 변경된 블록만 저장
- 비동기적 생성(수정된 블록이 S3로 모두 이동할 때까지 스냅숏 상태는 pending!)
- 사용 중인 볼륨도 스냅샷 생성할 수 있다(단, 루트 디바이스 역할의 EBS볼륨은 인스턴스 중지해야 한다)
- 무제한의 확장성, 빠른 복원, 빠른 확장성
- 데이터에 빠르게 액세스하고 장기적으로 지속해야 하는 경우에 적합
- 암호화: 암호화된 볼륨 및 스냅숏 생성 시 AWS KMS(Key Management Service) 고객 마스터 키(CMK) 사용
### EBS 볼륨 유형
- IOPS(Input Output Operations Per Second) 초당 입출력 작업을 나타냄
- SSD: 빠름
- HDD: 대용량

## EFS
- AWS 클라우드 서비스와 온프레미스 리소스에서 사용할 수 있는 간단하고 확장 가능하며 탄력적인 완전 관리형 탄력적 NFS 파일 시스템
- 애플리케이션 중단할 필요 없이 확장되므로 사용자가 용량을 프로비저닝 및 관리할 필요 없음
- 최대 수천 개의 EC2 인스턴스를 위한 스토리지이며 동시에 액세스 할 수 있다
- Network File System 프로토콜 사용
- VPC 내 EC2 인스턴스는 직접 액세스 할 수 있음
- On-premise 서버는 Direct Connect & VPN 연결을 통해 파일 시스템 탑재
- Direct Connect은 대역폭이 높고 지연 시간이 짧은 전용 네트워크 연결
- 암호화: AWS KMS(Key Management Service)에서 관리

## S3
- 웹에서 사용 가능한 object 저장소
- 뛰어난 내구성, 제약 없는 확장성
- 5가지 유형(Standard, Standard IA, One Zone IA, Glacier, Glacier Deep Archive)
