# Kubernetes object Pod
## Pod
- Kubernetes에서 관리하는 가장 작은 배포 단위
- `kubectl run echo --image [이미지주소]` = 이 이미지의 컨테이너를 가진 pod을 생성해주세요. 라는 뜻임.
- 1.18이상은 pod 이지만 1.17 이하는 deployment 만듬.
### Pod이 생성되는 과정
1. Scheduler는 API서버를 감시하면서 할당되지 않은unassigned Pod이 있는지 체크
2. Scheduler는 할당되지 않은 Pod을 감지하고 적절한 노드node에 할당 (minikube는 단일 노드)
3. 노드에 설치된 kubelet은 자신의 노드에 할당된 Pod이 있는지 체크
4. kubelet은 Scheduler에 의해 자신에게 할당된 Pod의 정보를 확인하고 컨테이너 생성
5. kubelet은 자신에게 할당된 Pod의 상태를 API 서버에 전달
## 명령어들을 알아보자
### 목록 조회
- `kubelctl get pod`
### 단일 Pod 상세 확인
- `kubectl pod/echo` <- 이름
- 위의 명령어를 입력하면 Pod 안에 클러스터, 클러스터 안에 echo 라는 이름을 가진 컨테이너가 생성됨.

### 삭제
- `kubectl delete pod/echo`

- 근데 이렇게 일일히 kubectl 하면서 관리하는 경우는 거의 없고, 더 편리하고 정교한 관리를 위해 yaml을 작성함.

### 필수 요소와 명령어
- 필수 요소 : version, kind, metadata, spec
- pod 생성 : kubectl apply -f echo-pod.yml
- Pod 목록 조회 : kubectl get pod
- Pod 로그 확인 : kubectl logs echo
- Pod 로그 실시간 확인 옵션 추가 : kubectl logs -f echo
- Pod 컨테이너 접속 : kubectl exec -it echo -- sh
- Pod 제거 : kubectl delete -f echo-pod.yml

## 마치며
- 컨테이너 생성과 실제 서비스 준비는 약간의 차이가 있음. 
- 서버를 실행하면 바로 접속하지 못하고 짧게는 수초, 길게는 수 분의 초기화 시간이 필요함
- 실제 접속이 가능하면 서비스가 준비되었다고 말할 수 있음.
- Pod을 단독으로 사용하는 경우는 거의 없고 Pod이 컨테이너를 관리하듯 다른 컨트롤러가 Pod을 관리함.
