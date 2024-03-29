# Jenkins 란
## Jenkins? 
젠킨스는 소프트웨어 개발 시 지속적으로 CI를 제공하는 툴이다. 다수의 개발자들이 하나의 프로그램을 개발할 때 버전 충돌을 방지하기 위해 각자 작업한 내용을 공유영역에 있는 저장소에 빈번히 업로드함으로써 지속적 통합이 가능하도록 해준다.

## 이점
코드의 변경과 함께 이뤄지는 이 같은 자동화된 빌드와 테스트 작업들은 다음과 같은 이점들을 가져다 준다.
- 프로젝트 표준 컴팡리 환경에서의 컴팡리 오류 검출
- 자동화 테스트 수행
- 정적 코드 분석에 의한 코딩 규약 준수여부 체크
- 프로파일링 툴을 이용한 소스 변경에 따른 성능 변화 감시
- 결함 테스트 환경에 대한 배포 작업

이 외에도 젠킨스는 수많은 플러그인을 온라인으로 인스톨 가능 + 파이썬과 같은 스크립트를 이용해 필요한 기능을 알잘딱 입맛대로 추가할 수 있다.

## 각종 배치 작업의 간략화
DB 구축, 어플리케이션 서버로의 Deploy, 라이브러리 릴리즈와 같이 이전에 CLI로 실행되던 작업들을 웹 인터페이스로 손 쉽게 가능하다.

## Build 자동화의 확립
젠킨스와 연동하여 빌드 자동화를 통해 프로젝트 진행의 효율성을 높일 수 있다.

## 자동화 테스트
자동화 테스트는 젠킨스를 사용해야 하는 가장 큰 이유 중 하나. Git 과 같은 버전관리 시스템과 연동하여 코드 변경을 감지, 자동화 테스트를 수행. 

## 코드 표준 준수 여부 검사
자동화 테스트와 마찬가지로 개인이 미처 실시하지 못한 코드 표준 준수 여부의 검사나 정적 분석을 통한 코드 품질 검사를 빌드 내부에서 수행함으로써 기술적 부채의 감소에도 크게 기여한다.

## 빌드 파이프라인 구성
2개 이상의 모듈로 구성되는 레이어드 아키텍처가 적용 된 프로젝트에는 그에 따른 빌드 파이프라인 구성이 필요하다. 젠킨스는 이러한 빌드 파이프라인의 구성을 간단히 할 수 있으며, 스크립트를 통해 매우 복잡한 제어까지도 가능하다.
