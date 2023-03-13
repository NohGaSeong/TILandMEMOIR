# Pod과 친해지기
**이 글은 패스트캠퍼스 DevOps 마스터 Kit With Linux, Kubernetes, Docker 강의를 들으며 작성되었습니다.**
## 이번 실습에서 진행할 것은?
1. Pod 선언과 환경변수 선언
2. Pod 생성/배포
3. pull image
4. Pod IP 할당 및 컨테이너 실행 확인
5. port-forward 3000:3000
6. pod으로 트래픽을 전송
7. http 서버 응답 확인
8. 컨테이너 환경변수 목록 확인

아래와 같은 json response 가 보여야함.

```.json
{
  "greeting": "Welcome to Kubernetes!",
  "host":{
    "name" : "gke-node",
    "ip":"10.128.0.15"
  },
  "namespace":{
    "name":"default"
  },
  "pod":{
    "name":"hello-app",
    "ip":"10.76.0.143"
  }
}
```

## Pod 선언과 환경변수 설정

```.yaml
# Pod 이름, 컨테이너 이름과 이미지, 포트를 설정해준다.
apiVersion: v1
kind: Pod
metadata:
  name:hello-app
spec:
  containers:
  - name : hello-app
    image : devchloe/hello-app:1.0
    ports:
    - containerPort:3000
    
# 환경변수와 키 값 설정
spec:
  containers:
  - env: hello-app
    - name : STUDENT_NAME
      value : 노가성
    - name : GREETING
      value : 안녕하세요, 제 이름은 $(STUDENT_NAME)입니다.
     
# Pod 오브젝트 값을 환경변수 값을 ㅗ설정
spec:
  containers:
  - env:hello-app
    - name : NODE_NAME
    valueFrom:  # '쿠버네티스 오브젝트로부터 환경변수 값을 얻겠다'
      fieldRef: # 'Pod spec, status의 field를 환경변수 값으로 참조하겠다.
        fieldPath: spec.nodeName  # 참조할 field의 경로 선택
    - name: NODE_IP
      valueFrom:
        fieldRef:
          fieldPath:status.hostIP
```

## Kubectl 명령어
- Pod 생성 : `kubectl apply -f <yaml 파일 경로>`
- pod 실행 및 IP 확인: `kubectl get pod -o wide`
- Pod 종료 : `kubectl delete pod --all` or `kubectl delete pod <pod-name>`
- 컨테이너 IP 확인 : `kubectl exec <pod-name> [-c <container-name>] --ifconfig ethO`
- 컨테이너 환경변수 확인 : `kubectl exec <pod-name> --env` -env 가 아니라 --env 임. 주의!
- 포트 포워딩 : `kubectl port-forward <pod-name><host-port>:<container-port>`

## 실습 진행
Pod이 잘뜨는것을 볼 수 있다.
![image](https://user-images.githubusercontent.com/82383294/224692716-8f3f22e5-91fc-4ec0-a0f8-230f217ae761.png)

