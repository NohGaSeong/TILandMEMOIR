# ELK
## ELK?
- ELK = Elastic Search + LogStatsh + Kibana 를 말함. 데이터 수집 및 분석 툴임.
- 높은 확장성과 뛰어난 이식성을 가지고 있어 다른 여러가지 툴과도 연동이 가능함.

## 어떤 소프트웨어를 사용함?
### LogStatsh
- 수집할 로그를 선정, 지정된 대상 서버에 인덱싱해서 전송하는 역할을 담당하는 소프트웨어. 다양한 플러그인 제공을 여러 유형의 로그 수집 및 인덱싱이 가능함.
- 여러 소스의 데이터를 동시에 가져와서 변환한 다음 Elasticsearch와 같은 stash로 보내는 서버 측 데이터 처리 파이프라인임.

### Elastic Search
- ElaticSearch 는 Lucene 기반으로 개발한 분산 검색엔진임.
- LogStash 를 통해 수신된 데이터를 저장소에 저장하는 역할을 담당.
- RDB와 비슷하나 성능은 훨씬 뛰어남.

### Kibana
- Kibana는 사용자에게 분석 결과를 가시적으로 보여주기 위한 목적으로 만들어진 소프트웨어임.
- Elasticsearch에서 차트와 그래프로 데이터를 시각화 할 수 있음.

### ++ beats
- 단일 목적의 데이터 수집기 플랫폼입니다.

## Data Flow 는?
1. 1개 이상의 수집할 Data 발생 서버에서 beats가 특정 트리거에 의해 logstash로 Data를 전송합니다. 여기서 각 Client서버 마다 Beats가 설치되어 있어야합니다.
2. logstash로 전달 된 Data를 커스터마이징이 가능한 필터를 통해 가공하여 Elasticsearch로 전달함.
3, Elasticsearch로 전달 받은 데이터를 서버(Elasticsearch)에 저장함.
4. kibana에서 연동되있는 Elasticsearch에 저장된 데이터 셋을 토대로 시각화 제공

 
