## 개요
프로젝트 배포를 진행하기 위해 빌드를 진행하던 와중 아래와 같은 오류가 뜨며 빌드가 진행되지 않았다. 
<img width="885" alt="image" src="https://github.com/NohGaSeong/TILandMEMOIR/assets/82383294/86f2299c-d70f-4731-9076-27575d7818af">
그래서 백엔드 챕터를 맡고있는 팀원에게 물어보니 ./gradlew bootjar 로 빌드를 해보란다. 그래서 그냥 했더니
![](https://velog.velcdn.com/images/noyohanx/post/79f24fe1-9f33-473d-83dc-725874b2b1b5/image.png)

어레 왜 되냐 이거 제대로 빌드가 안된거 아닐까 하고 실행해보니 
<img width="749" alt="image" src="https://github.com/NohGaSeong/TILandMEMOIR/assets/82383294/98ea1e92-37ad-4fde-b360-4f6ff4d224b0">실행까지 잘 돼서 이게 대체 뭐가 다른걸까 하고 궁금증이 들어 조사하고 공부해보게 되었다.![](https://velog.velcdn.com/images/noyohanx/post/b3dde55a-ad6f-4905-be4a-d850b20ba014/image.png)

## Gradle build
gradle build는 bootjar과 달리 내부 동작이 더 많으며 길다.(그 내부동작에 bootjar도 포함되어있다) build는 test 코드가 있다면 테스트도 수행을한다.

모든 테스트 실행, 프로덕션 아티팩트 생성 및 문서 생성을 포함하여 모든 것을 구축하기 위한 것이다.

build가 bootjar과 다른 것들이 여러 가지가 있는데 그 중 가장 대표적인건 lift cycle과 관련된 task가 존재한다는 것이다. 그 중 check, assembel 작업이 있는데 check 로 test 코드 이외의 확인 작업을 한 번 더 하고 assemble을 통해 프로젝트의 결과물을 내는 모든 작업을 단일 작업으로 만들어 결과물을 만든다.

그러기에 assemble과 check를 사용하여 구체적인 작업을 하기 위해 사용한다.

## Gradle boojar
단순히 프로젝트의 jar 파일만을 만드는데 목적을 가지고 있다. 그만큼 빌드하는데 속도도 빠르다.

jar 빌드에만 집중하고 싶고? 테스트 실행, 코드 적용 범위, 정적 코드 분석, 수명 주기 check 작업등의 항목들을 별로 신경쓰지 않을때 사용된다.

## 마치며
위에서의 언급한 gradle build 에러는 아마도 테스트 코드가 제대로 작성되지 않아 생긴 에러가 아닌가 싶다. bootjar 이라도 사용해서 빌드가 잘 돼서 일단은 ok 이지만 결국엔 그냥 build 를 사용하여 빌드를 하는게 훨씬 더 좋지 않을까 싶어 백엔드 챕터 팀원들에게 내가 공부하여 정리한 글을 전달할 에정이다.
