# BuildSpec 이란?
## BuildSpec 이란?
- CodeBuild에서 구축을 수행하는 데 필요한 buildspecyml 파일.
- 저 파일을 참고해서 build 를 진행함. 
- github action 의 yml workflow 랑 비슷? 하다고 보면됨.

## 예시
```
version: 0.2

phases:
  install:
    runtime-versions:
      java: corretto11
  pre_build:
    commands:
      - echo Nothing to do in the pre_build phase...
  build:
    commands:
      - echo Build started on `date`
      - mvn install
  post_build:
    commands:
      - echo Build completed on `date`
artifacts:
  files:
    - target/messageUtil-1.0.jar
```
