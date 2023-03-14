# label과 selector
## 개념
Label : 쿠버네티스 오브젝트를 식별하기 위한 key/value 쌍의 메타 정보
Selector :  Label을 이용해 쿠버네티스 리소스를 필터링하고 원하는 리소스 집합을 구하기 위한 label query
<br>
클러스터에서 서로 다른 팀의 수백개 Pod이 동시에 실행되고 있는 상황에서 주문 트래픽을 주문 Pod으로, 배달 트래픽을 배달 Pod으로 라우팅해야할때
<br>
우리가 어떤 리소스를 선택해서 명령을 실행하고자 할 때 Label과 Selector를 이용한다.
- Label : 쿠버네티스 리소스를 논리적인 그룹으로 나누기 위해 붙이는 이름표
- Selector : Label를 이용해 쿠버네티스 리소스를 선택하는 방법 (label query)

## Label
```.yaml
apiVersion : v1
kind: Pod
metadata:
  name : my-pod
  labels: # 요 label 을 이용하여서 my-pod 을 식별할 수 있음.
    app: backend
    version : v1
    env:prod
spec:
  containers:
  - image:my-pod
    name : my-pod
```
### label로 식별하기
`$ kubectl label pod my-pod app=backend`
`$ kubectl get pod my-pod --show-labels` 를 하면
<img width="308" alt="image" src="https://user-images.githubusercontent.com/82383294/224992638-7f9b0d82-d9a8-4204-8430-d2ba268aa7d9.png"> 
요렇게 레이블이 알잘딱 보인다.

### label 수정하기
`$ kubectl label pod my-pod version=v1`
`$ kubectl label pod my-pod version=v2 --overwrite`
pod/my-pod labeled

### label key 선택 출력 명령어와 옵션
`$ kubectl get pod/my-pod --label-columns app.env`
<img width="327" alt="image" src="https://user-images.githubusercontent.com/82383294/224993237-a98da558-b85a-445a-a0d6-a37f9429bb25.png">
아래 명령어처럼 줄여서 표현도 가능함

### label 삭제 명령어와 옵션
`$ kubectl label pod/my-pod app-`
`$ kubectl get pod/my-pod --show-labels`
<img width="367" alt="image" src="https://user-images.githubusercontent.com/82383294/224994000-3be0a5ed-9a88-4e60-a5ba-e5876752645f.png">

## Selector
### kubectl get 명령어와 함께 selector 를 사용하는 방법
- `kubectl get <오브젝트 타입> --selector <label query 1, ... , label query N>`
- `kubectl get <오브젝트 타입> -l <label query 1, ... , label query N>`
- label query:key=value

### Equality-Based Selector
- 같다(=), 같지 않다 !=
- Key=Value:key 값이 value일 때
- key!=value:key 의 값이 value가 아닐때

### Pod과 Label의 조회
<img width="270" alt="image" src="https://user-images.githubusercontent.com/82383294/225159694-aa8e34c6-bb10-4a18-af82-b4c3b8835e86.png">


### selector 옵션을 이용한 Pod 조회
<img width="276" alt="image" src="https://user-images.githubusercontent.com/82383294/225159718-a6891aca-ce23-4a10-9ca4-2736ec991f32.png">


### 새로운 Label 추가
`$ kubectl label pod pod1 pod2 pod3 app=backend`
<img width="364" alt="image" src="https://user-images.githubusercontent.com/82383294/225159778-9c917bab-1454-4427-8cec-31c4636d57c3.png">


### Set-Based Selector
- 값이 어떤 집합에 속해 있다/속해 있지 않다(OR 연산 가능)
  - 'key in(value1, value2, ...)':key의 값이 value1 이거나 value2 일떄
  - 'key notin(value1, value2, ...)' : key의 값이 value1 이 아니거나 value2가 아닐때
- 키가 존재한다/존재하지 않는다.
  - 'key' : label 에 key가 있을 때
  - 'key' : label 에 key가 없을 때 

## 요약
- 쿠버네티스 오브젝트 metadata.labels 속성으로 리소스에 Label을 추가할 수 있다.
- Label은 key/value 쌍으로 선언한다.
- 쿠버네티스 오브젝트에 선언한 Label의 key, value를 기준으로 원하는 리소스를 필터링할 수 있다.
- 필터링 하기 위한 조건을 selector 로 정의한다(label query)
- 즉 label과 selector를 사용하면 특정 리소스들의 집합을 구할 수 있다.
- kubectl get 명령어를 사용할 때 label query를 지정하기 위해 --selector 또는 -l 옵션을 사용한다.

