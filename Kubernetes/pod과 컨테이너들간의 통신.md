## 실습 내용
1. Pod 선언과 환경변수 설정
2. Pod 생성/배포
3. Pod IP 할당 및 컨테이너 실행 확인
4. 컨테이너 환경변수 목록 확인
5. 컨테이너 간 localhost 통신
6. 다른 pod 의 pod ip로 통신
7. 포트포워딩을 통해 각 컨테이너로 요청/응답 확인

## 명령어 또 알아보고 가자
- pod 생성 : `kubectl apply -f <yaml 파일 경로>`
- pod 실행 및 ip 확인 : `kubectl get pod -o wide`
- pod 종료 : `kubectl delete pod --all or kubectl delete pod <pod-name>`
- 컨테이너 간 통신 : `kubectl exec <pod-name> -c <container-name> -- curl -s localhost:<container-port>`
- pod 간 통신 : `kubectl exec <pod-name> -c <container-name> --curl -s <pod-ip>:<container-port>`
- 컨테이너 로그 출력 : `kubectl logs <pod-name><container-name>`
- 컨테이너 Ip 확인 : `kubectl exec <pod-name> -c <container-name> --ifconfig eth()`
- 컨테이너 환경변수 확인 : `kubectl exec <pod-name> --printenv`
- 포트 포워딩 : `kubectl port-forward <pod-name><host-port>:<container-port>`

## yaml 파일들
```.yaml
apiVersion : v1
kind: Pod
metadata:
  name : red-app
spec:
  containers:
  - name : red-app
    image : yoonjeong/red-app:1.0
    ports :
    - containerPort : 8080
    env : 
    - name : NODE_NAME
      valueFrom : 
        fieldRef : 
          fieldPath : spec.nodeName
    - name : NAMESPACE
      valueFrom:
        fieldRef:
          fieldPath: metadata.namespace
    - name : POD_IP
      valueFrom:
        fieldRef :
          fieldPath: status.podIP
    resources:
      limits:
        memory: "64Mi"
        cpu: "250m"
 ```
 ```.yaml
 # Pod API 버전: v1
# Pod 이름: blue-green-app
# 컨테이너 이름/포트: blue-app(8080)
# 도커 이미지: yoonjeong/blue-app:1.0
# 환경변수: NODE_NAME, NAMESPACE, POD_IP 설정
apiVersion : v1
kind: Pod
metadata:
  name : blue-green-app
spec:
  containers:
  - name : blue-app
    image : yoonjeong/blue-app:1.0
    ports :
    - containerPort : 8080
    env : 
    - name : NODE_NAME
      valueFrom : 
        fieldRef : 
          fieldPath : spec.nodeName
    - name : NAMESPACE
      valueFrom:
        fieldRef:
          fieldPath: metadata.namespace
    - name : POD_IP
      valueFrom:
        fieldRef :
          fieldPath: status.podIP
    resources:
      limits:
        memory: "64Mi"
        cpu: "250m"
  - name : green-app
    image : yoonjeong/green-app:1.0
    ports :
    - containerPort: 8081
    env : 
    - name : NODE_NAME
      valueFrom : 
        fieldRef : 
          fieldPath : spec.nodeName
    - name : NAMESPACE
      valueFrom:
        fieldRef:
          fieldPath: metadata.namespace
    - name : POD_IP
      valueFrom:
        fieldRef :
          fieldPath: status.podIP
    resources:
      limits:
        memory: "64Mi"
        cpu: "250m"
```
```
kubectl exec blue-green-app -c green-app -- curl -vs localhost:8080/sky
```
```
export BLUE_POD_IP=$(kubectl get pod blue-green-app -o jsonpath="{.status.podIP}")
echo $BLUE_POD_IP
kubectl exec red-app -- curl -vs $BLUE_POD_IP:8080/sky
kubectl exec red-app -- curl -vs $BLUE_POD_IP:8080/hello
```
위의 명령어들로 통신을 시도하면 잘 되는 것을 볼 수 있다.
<img width="662" alt="image" src="https://user-images.githubusercontent.com/82383294/224987865-3a492d52-3fc4-4d50-9647-1180ae8f9265.png">

## 결과
curl localhost:포트 를 입력해주니 잘 뜨는 모습이다!
<img width="703" alt="image" src="https://user-images.githubusercontent.com/82383294/224987175-7d7bdaec-493b-4f64-9c34-5846dd33227b.png">
