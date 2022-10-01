# 쿠버네티스 기초_API 호출
## object spec _ YAML
### pod의 object spec
```.yaml
api version : v1
kind : pod
metadata:
  name : example
spec:
  containers:
  - name:busybox
    image:busybox:1.25
```

### replicaset의 object spec
```.yaml
apiversion:apps/v1
kind:replicaset
metadata:
  name : frontend
spec:
  replicas : 3
  selector:
    matchLabels:
      app : frontend
  template:
    metadata:
      lables:
        app : frontend
    spec:
      containers:
      - name : web
        image : image:v1
```

### Object Spec 설명
- apibersion : apps/v1, v1, batch/v1, networking 등
- kind : pod,deployment,service,ingress 등
- metadata: -name, lable,namespace 등
- spec : 각종 설정들
- status(read-only) : 시스템에서 관리하는 최신상태

## 결론
### API 호출하기는
- 원하는 상태를 다양한 object 로 정의하고, API 서버에서 yaml 형식으로 전달해주는 것.
  
