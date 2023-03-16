# 카카오엔터프라이즈가 Github Actions를 사용하는 이유
https://tech.kakao.com/2022/05/06/github-actions/ </br>
위의 글을 보고 작성한 글입니다.

## 카카오엔터프라이즈 DevOps 표준안
깃허브 Enterprise -> github action을 통해 CI 과정을 진행함. 이때 소스가 이미지 형태로 생성되면 카카오 i 클라우드의 컨테이너 레지 스트리에 업로드.
업로드된 이미지는 argo Cd를 통해 배포하며, 배포 타깃은 카카오 i 클라우드의 쿠버네티스 엔진임.

## Github Actions
기존 카카오엔터프라이즈의 경우 jenkins, drone, bamboo 등 여러 CI 솔루션을 사용하고 있었음. 각 프로젝트마다 각기 다른 솔루션을
사용하다보니 여러가지 문제 발생.<br>


또한 여러프로젝트가 협업을 할 때 하나의 CI 툴로 통합해서 CI 작업을 진행해야하는 어려움. 그 CI 를 수행함에 있어서 ci 툴에 맞는 문서 작성을 위한 문법 
숙지도 필요했음. 이러한 이슈들로 인해 지속적인 허들 발생. => 그래서 깃허브 액션이라는 하나의 ci 솔루션을 도입.

### Github Actions을 카카오 엔터프라이즈 CI 솔루션으로 채택하게 된 이유
1. 깃허브와 하나로 통일된 환경에서 ci 수행이 가능함.
2. 중앙에서 관리하는 github actions runner에 지속적으로 트러블 슈팅을 하여 원활한 ci 환경 구성이 가능함.
3. 프로젝트마다 개별 runner를 통한 빌드 테스트가 가능함.
4. gtihub actions runner 기동을 하기 위해 친숙한 문법인 yaml 파일로 간단하게 파이프라인 구성이 가능함.

## Github Actions Runner
Github는 퍼블릭 쪽의 github actions runner 를 클라우드에서 제공해주고 있음. 그래서 직접 프로비저닝할 필요 없이 runner 를 바로 사용 가능함.
하지만 사정으로 인해 별도로 로컬에 있는 actions runner나 중앙에서 프로비저닝하는 actions runner로 github actions 를 수행함. 

## self hosted runner
self-hosted runner를 직접 ui에서 만들 수 있음. 각 repository의 settings 페이지에는 actions > runner 상세 페이지가 있음.
이 페이지에서 runner 를 생성하면 서버 뿐 아니라 로컬 환경에서도 self-hosted Runner 를 설치해 분석할 수 있음.

## Action Runner List 확인
링크의 이미지를 봐보면 runs-on 이라는 k8s 라벨을 찾아서 Action Runner가 기동하는 형태. 그리고 k8s runner 라벨 오른쪽에 status가 idle, active 이런식으로 있는데 하나는 작업이 
할당되어 진행중인거고, 하나는 작업을 할당할 수 있는 runner 임

## 나머지
나머지는 github action 의 기본적인 내용들을 설명해주는 글이였다.

## 글을 읽고 느낀점
이런 현역 개발자, 엔지니어분들의 경험이 담긴 글들을 읽음으로써 많은 것을 깨닫고, 얻어가는 것 같다. 기존에 자주 쓰던 서비스이고, 사용하기 편해서 기업들은 git actions 를 잘 사용하지 않겠지 라는 생각을 하였는데 
그런 생각을 부숴준 글이였고. action runner? 등 사용해보지 못한 옵션, 서비스들을 알아가서 저것들에 대해서 좀 더 공부해보고, 실습한 다음, 또 프로젝트를 진행하게된다면 그때 적용시켜보고 싶다.
