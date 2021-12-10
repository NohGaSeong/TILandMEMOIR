# GitHub Action 을 이용한 CICD
## GitHub Action
- CI/CD 를 가능하게 해주는 툴 중 하나.
- 이외의 툴들 : Jenkins, AWS Code Deploy, GCP의 Code Build 등
- GitHub 레파지토리에 Action 탭을 누르면 사용 가능
- 그 후 자동화된 서비스를 만들기 위해서는 workflow라는 걸 만들어야한다.

## Workflow
- 자동화된 프로세스를 만들기 위한 Yaml 파일
- 확장자 = .yml, .yaml
- Workflow를 알기 위해선 해당 개념들이 있는데 workflow > job > step > action 순으로 명시해서 파일 작성해야함

### workflows
- 레파지토리에 정의한 자동화된 프로세스 절차
- 하나 이상의 Jobs 로 구성되고 이벤트 기반으로 트리거됨
- ex) schedule 을 설정해 정해진 시간에 실행되도록 하거나 main 브런치에 코드가 push가 되거나 어떤 브런치에 pull request
가 만들어지면 실행되도록 설정 가능 + webhook 을 이용해 외부 이벤트에 대한 응답으로 실행 가능

### Jobs
- 하나 이상의 steps 로 구성되고 workflow에있는 job 끼리는 병렬적으로 실행된다.
- job 끼리는 순서대로 실행되도록 설정할 수 있다.
- ex) job은 build 과정을 실행하고 다른 job은 test 를 실행하도록 명시하고 test job은 build가 완료된 후 실행하도록 할 수 있다.
+ 이때 두 job 끼리는 다른 환경에서 실행되므로 같은 스토로지를 사용하도록 설정해야한다.

### Steps
- 하나의 step은 하나의 task 라고 생각하면된다. 
- 하나의 job에 여러 task를 넣을 수 있다.
- step은 action 이나 shell command로도 생성될 수 있다.
- 하나의 job에 있는 step은 같은 runner에 의해 실행된다.

### Actions
- workflow에서 가장 작은 개념으로 action은 독립된 실행할 명령이라고 생각하면된다.

### Runners
- GitHub에 호스팅되고 있는 서버이다. 이걸 통해 job을 실행시킨다.    

## 예제
```.yml
name : learn-github-actions

on:
  push:
    branches: [master]
  pull_request
    brancehs: [master]
    
 jobs:
  check-bats-version:
    runs-on: unbuntu-latest
    
    steps:
      - uses : actions/checkout@v2
      - uses : actions/setup-node@v1 
      
      - run : npm install -g bats
      - run : bats -v
```
- name : learn-github-actions : workflow 이름
- on: push, pull_request : 이 workflow가 trigger될 이벤트를 명시한다. 
- jobs : 실행할 job
- check-bats-version : job의 이름
- runs-on:ubuntu-latest : job이 돌아갈 환경
- steps : 하나의 job에서 실행할 step 을 명시
- uses:actions/checkout@v2 : 다른 오픈 소스 커뮤니티에 있는 actions를 가지고 와서 실행하라고 job에게 알려주는것.
- uses:actions/setup-node@v1 : 이 uses는 runner에 node 패키지를 설치
- run:npm install -g bats : command 로 실행할 명령
- run : bats-v : 위와 같음

## GitHub Actions workflow - matrix build
- Github Action에서는 여러 환경을 동시에 빌드 가능 = matrix build 라고 부름
```
jobs:
  build:
    runs-on:ubuntu-lastest
    
    strategy:
      matrix:
        os: [unbuntu-latest, windows-2016]
        node-version:[12.x,14.x]
```

## GitHub Action build artifact
- GitHub action에서 job을 빌드와 테스트로 분리햇다면 서로 다른 환경을 가지고 있는 거임
- 그러므로 Built-in 아티팩트 스토로지를 이용해 빌드 아티팩트를 서로 공유해야함
- 사용할 때 주의 할 점 : job을 순서대로 동기화해서 진행시켜야함

```
jobs:
  job_1:
    name: Add 3 and 7
    runs-on: ubuntu-latest
    steps:
      - shell: bash
        run: |
          expr 3 + 7 > math-homework.txt
      - name: Upload math result for job 1
        uses: actions/upload-artifact@v2 # built-in 아티팩트 스토로지에 업로드 한다. 
        with:
          name: homework
          path: math-homework.txt

  job_2:
    name: Multiply by 9
    needs: job_1 # job_1이 끝난후에 실행하도록 명시했다. 
    runs-on: windows-latest
    steps:
      - name: Download math result for job 1 
        uses: actions/download-artifact@v2 # 아티팩트 스토로지에서 다운로드 한다. 
        with:
          name: homework
      - shell: bash
        run: |
          value=`cat math-homework.txt`
          expr $value \* 9 > math-homework.txt
      - name: Upload math result for job 2
        uses: actions/upload-artifact@v2
        with:
          name: homework
          path: math-homework.txt
 ```
