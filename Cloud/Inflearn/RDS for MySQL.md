# RDS for MySQL 생성하기

## 1. 아키텍처에 구현할 기술
완전 관리형 MySQL 데이터베이스를 구성하고 Linux 기반의 가상 서버에서 MySQL 클라이언트로 연결합니다.

### 필요 AWS 서비스
- Amazon Relational Database Service(RDS)

### 기타 필요 사항
- 간단한 Query문 및 PHP 문법

## 아키텍쳐 구현 순서
1. RDS for MySQL 구성하기<br>
   (1). Database creation method 선택<br>
   (2). Database Engine 선택<br>
   (3). DB 식별, Master Username/PW 셋팅<br>
   (4). DB Instance size 선택<br>
   (5). 네트워크 설정<br>

2. RDS for MySQL을 EC2에 연결하기.<br>
    (1).PuTTY를 이용하여 Bastion에 SSH 연결<br>
    (2). MySQL 클라이언트를 통해 연결<br>

    