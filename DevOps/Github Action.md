# Github Action
## 기존에 작성한걸 왜 또 작성하는거임
- 쓸 기회가 많이 없다보니까 기억이 안나게 되었다.
- 복습한다는 느낌으로 기초와 응용, 그리고 실습까지 적어볼려고한다.

## GithubAction 이란?
- 소프트웨어 workflow 를 자동화 할 수 있도록 도와주는 도구

### workflow의 대표적인 예
- test code
- 배포
- 자동화하고 싶은 스크립트
- 다양한 버전에서 실행되는지 확인

## Github Action Core 개념
### Workflow
- 여러 job 으로 구성되고, event에 의해 트리거 될 수 있는 자동화된 프로세스
- 최상위 개념
- workflow 파일은 yaml 으로 작성되되고, Github Reopository dml `.github/workflows` 폴더 아래에 저장됨

### Event
- Workflow 를 Trigger 하는 특정 활동, 규칙
#### 예를 들어?
- 특정 브랜치로 push
- 특정 브랜치로 pull request 하거나
- 특정 시간대에 반복(cron)
- webhook 을 사용해 외부 이벤트를 통해 실행

### Job
- Job은 여러 Step 으로 구성되고, 가상 환경의 인스턴스에서 실행됨
- 다른 Job에 의존 관계를 가질 수 있고, 독립적으로 병렬 실행도 가능함

### Step
- Task 들의 집합. 커맨드를 날리거나 action 을 실행할 수 있음.

### Action
- workflow 의 가장 작은 블럭
- job 을 만들기 위해 step 들은 연결 할 수 있음
- 재사용이 가능한 컴포넌트
- 개인적으로 만든 Action 을 사용할 수도 있고, Marketplace에 있는 공용 Action 을 사용할 수도 있음.

### Runner
- Github Action Runner 어플리케이션이 설치된 머신으로, Workflow 가 실행될 인스턴스
- Github에서 호스팅해주는 Github-hosted runner와 직접 호스팅하는 Self-hosted runner로 나뉨.

## Github Action 생성하는 흐름.
- 코드를 작성
- Workflow 정의
- 정상 작동하는지 Test

### workflow 정의하기
- `.github/workflows` 폴더 안에 `.yml` 파일을 생성 (템플릿 활용하시면 좋습니다.)

### 예제
- Master 브랜치에 push 또는 pull request 가 올 경우 실행되는 CI 란 이름을 갖는 workflow

```
name : CI

on :
    push : 
        branches: [ master ]
    pull_request:
        brnaches: [ master ]

jobs:
    build:
        runs-on : ubuntu-latest

        steps:
        - uses : actions/checkout@v2
        
        - name : Run a one-line script
          run : echo Hello, World!

        - name : Run a multi-line script
          run: |
            echo Add other actions to build,
            echo test, and deploy your project.
```
- name : workflow의 이름을 지정
- on :
    - event 에 대해 작성하는 부분 
    - 어떤 조건에 workflow 를 trigger 시킬지
    - push(Branch or Tag), pull_request, schedule 을 사용할 수 있음.
    - 단일 event 를 사용할 수도 있고, array 로 작성할 수도 있음.
    ```
    on:push
    # 또는 
    on : [pull_request, issues]
    ```
- jobs: 
    - workflow 는 다양한 job 으로 구성됨
    - 여러 job이 있을 경우, default로 병렬 실행
    - build 라는 job 을 생성하고, 그 아래에 2개의 step 이 존재하는 구조
    - runs-on은 어떤 os 에서 실행될지 지정
    - strategy - matrix 인자를 사용하면 어떤 버전에서 테스트할지 확인할 수 있음.
    - run 할 때 env(환경변수)를 설정하는 예제가 없음. 따로 정리하자.
    - stops 의 uses는 어떤 액션을 사용할지 지정함. 이미 만들어진 액션을 사용할 때 지정.

## 엄청 쉽다 라고 말할 도구는 아닌지라 계속 추가해나가겠음

_ github 연동 테스트 _ 3번째. 제발 되라