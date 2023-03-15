# label과 selector 실습
## 과정
1. Label과 함께 pod 선언
2. Pod 생성/배포
3. kubectl 명령어로 pod 에 label을 추가/변경/삭제
4. pod에 선언한 label 확인
5. selector로 배포한 pod 의 부분집합 조회


### label 추가/조회
- 각 파드에 concept, position, version 레이블 추가
- group=nature 레이블을 가진 모든 파드 조회
- concept가 flower이거나 earth인 모든 파트 조회
- concept 레이블이 없는 모든 파드 조회(!,notin 이용)

### 작업 실행을 위한 모든 파드 조회
- 물을 주어야 하는 group=nature 레이블을 가진 모드 파드 조회 (position=bottom)
- 손이 닿지 않는 group=nature 레이블을 가진 파드의 ip 조회(position=top)

### Label 변경/삭제
- elemenet=tree 레이블을 가진 모든 파드를 concept=mountain 레이블로 변경
- group=greeting 레이블을 가진 파드에서 version 레이블 삭제

## 실습
잘되는것을 볼 수 있다.
<img width="711" alt="image" src="https://user-images.githubusercontent.com/82383294/225247904-0fb7d0b5-2e9b-4249-b42f-75e6cd5e38ee.png">
<img width="623" alt="image" src="https://user-images.githubusercontent.com/82383294/225247962-423be7f9-a1ee-4344-a3fe-19deb8e7940f.png">
