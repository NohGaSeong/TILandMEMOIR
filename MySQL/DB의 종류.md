# DB 의 종류

## 관계형 데이터베이스

80년대부터 흥하기 시작해서 아직까지도 사용하고 있는 데이터베이스의 표준 같은 데이터베이스. 짧게 요약하자면 엑셀처럼 행과 열로 데이터를 저장할 수 있는 데이터베이스를 뜻합니다 .

어떤식으로 생겼을까?
엑셀의 시트처럼 생긴 테이블이라고 부르는 공간을 하나 생성한 다음 행과 열에 맞춰 데이터를 쭉 저장합니다. 생긴 것도 엑셀임

특징

- 거의 모든 곳에 사용할 수 있어 범용적이다.
- 구조화된 데이터를 저장하기 가장 좋다
- 보통 sql 이라는 언어를 이용해 데이터를 출력 입력한다.
- 이 열엔 숫자가 들어옵니다 ~ ㅏ고 스키마를 미리 정의하기 때문에 관리가 쉽다.
- 구조화된 데이터 덕분에 원하는 데이터 뽑기도 쉽다
- 트랜잭션 롤백 이런 기능을 이용해 데이터의 무결성을 보존하기 쉽기 때문에 금융, 거래 서비스에 필수이다.

## Relational 의 뜻

데이터들 간의 관계를 정해서 데이터를 저장할 수 있다라는 뜻이다.


## NoSQL 데이터베이스

### 정의

- SQL 문 없이도 사용할 수 있는 데이터베이스
- 대부분 테이블에 국한되지 않고 자유로운 형식으로 데이터를 쉽게 분산 저장할 수 있다.

### 종류
- key-value 모델 : object, json 자료형 형식으로 데이터를 쉽게쉽게 저장, 출력 가능. 가장 심플
- document 모델 : 테이블 대신 collection 이라는 문서 기반으로 데이터를 분류하고 저장. 테이블보다 훨씬 유연함.
- graph 모델 : 데이터를 노드의 형태로 저장하고 노드간의 흐름또는 관계를 저장할 수 있음
- wide-column 모델 : 한 행마다 각각 다른 수, 다른 종류의 열을 가질 수 있음. (스키마가 자유롭다)

### 특징

1. scaling 이 쉬움
- 찰나의 순간에 대량의 데이터를 저장해야한다면 어케해야할까?
기존 오래된 관계형 데이터베이스는 확장이 어려움. 보통 scale up 이라는 방법으로 서버의 성능을 키워야함. 
 하지만 대부분의 noSQL 데이터베이스는 scale out 이라는 방법으로 데이터를 분산저장하는 걸 기본적으로 지원함. 확장 걱정할 필요없이 쉽게쉽게 데이터 입출력에만 신경쓸 수 있음. 그래서 대량의 데이터를 빠르게 입출력해야한다면 noSQL 이 제격임.
1. 대부분 다루기 쉽다.
- SQL 이라는 언어를 새로 배우지 않아도 데이터를 쉽게 입출력할 수 있다.
자바 스크립트 object{} 자료형 다루듯이 데이터를 입출력할 수 있으니 사용자에게 매우 편리.
그리고 서버에서 쓰던 프로그래밍 언어로 db 를 다룰 수 있다는 장점이 있음.
1. 대부분 스키마 정의 없이도 쉽게 쓸 수 있음.
- 양날의 검. 그래서 mongoDB에선 스키마를 미리 정의하기 위한 Mongoose 같은 라이브러리를 추가해서 사용하기도함
1. noSQL 데이터베이스는 기본적으로 sql 에서의 join 연산을 적용하는게 기본적으로 어려움. 서버 단에서 join 연산을 쉽게 처리해주는 라이브러리를 이용.

두 데이터베이스가 공존하는 이유는 서로 장점이 명확히 다르기 때문.
정규화된 데이터와 안정성 -> 관계형 데이터베이스
금융 서비ㅅ, 은행 전산 시스템 -> 안정적인 관계형이 최고

일초에 수백만개의 데이터 입출력 요청이 들어오는 sns 서비스를 만들때
서비스의 변경사항이 잦아서 쉽고 유연하게 데이터를 저장하고 싶으면 noSQL 을 사용
