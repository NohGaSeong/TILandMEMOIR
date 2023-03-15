# Pod NodeSelector 실습
## 실습 준비
### Pod에 원하는 노드 집합에 배포할 수 있음.
- 노드에 Label 추가
- Pod YAML 파일에 spec.nodeSelector를 선언

과정을 보자
1. 노드에 Label 추가
2. kubectl 명령어로 노드 레이블 확인
3. Pod 선언 시 nodeSelector 정의
4. Pod 생성/배포
5. Pod이 배포된 노드 확인

### 노드 설정 
노드 목록 조회
`$ kubectl get node`

노드에 Label 추가
`$ kubectl label node gke-8bbe0b49-0g80gke-8bbe0b49-bk10 soil=moist`
`$ kubectl label node gke-8bbe0b49-75xs soil=dry`


### Pod NodeSelector 선언 및 생성
kubectl run 명령어를 통한 Pod 선언과 생성
- `$ kubectl run <pod-name> --image <image-name>`
- 특정한 이미지를 Pod으로 생성하고 YAML 파일 정의없이 간편하게 실행할 수 있다.

soil=moist 레이블을 가진 모든 노드에 Pod 배포
```
$ kubectl run tree-app-1 \
--labels="element=tree" \
--image=yoonjeong/green-app:1.0 \
--port=8081 \
--overrides='{"spec":{"nodeSelector":{"soil":"moist"}}}'
```

### 이것들을 기억하자!
Label 선언
- metadata.labels 속성

Label 추가/변경/확인 명령어
- `$ kubectl label <resource-type>/<resource-name>key=value (--overwrite)`
- `$ kubectl get <resource-type>/<resource-name> --show-labels`
- `$ kubectl get <resource-type>/<resource-name> -L <key,...>`

Label Selector로 리소스 집합을 선택하는 명령어
- `$ kubectl get <resource-type> --selector <key=value,...>
- `$ kubectl get <resource-type> --selector <'key in/notin (value, ...)'>`
- `$ kubectl get <resource-type> --selector <key | '!key'>`
