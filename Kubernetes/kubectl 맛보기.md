## Kubectl 명령어 실습
`kubectl api-resources`
- 쿠버네티스 클러스터에서 사용할 수 있는 오브젝트 목록 조회

`kubectl explain (type)`
- 쿠버네티스 오브젝트의 설명과 1레벨 속성들의 설명
- apiVersion, kind, metadata, spec,status
  
`kubectl explain (type).(fieldName)[.(fieldName)]`
- kubectl explain pods.spec.containers
- 쿠버네티스 오브젝트 속성들의 구체적인 설명(Json 경로)

`kubectl get nodes`
- 쿠버네티스 클러스터에서 속한 노드 목록 조회

`kubectl apply -f (object-file-name)`
- kubectl apply -f deployment.yaml
- 쿠버네티스 오브젝트 생성/변경

`kubectl get pods`
- 실행 중인 Pod(컨테이너) 목록 조회

`kubectl scale -f (object-file-name) --replicas=#`
- kubectl scale -f deployment.yaml --replicas=3
- 애플리케이션 배포 개수를 조정 (replicas:복제본)

`kubectl diff -f (object-file-name)`
- kubectl diff -f deployment.yaml
- 현재 실행 중인 오브젝트 설정과 입력한 파일의 차이점 분석

`kubectl edit (type)/(name)`
- kubectl edit deployment/nginx-deployment:replicas를 4로 변경
- 쿠버네티스 오브젝트의 spec을 editor로 편집 

`kubectl port-forword (type)/(name) (local-port):(container port)`
- kubectl port-forward pod/nginx-deployment-74bfc88f4d-fkfjc 8080:80
- 로컬 포트느느 파드에서 실행 중인 컨테이너 포트로 포워딩

`kubectl attach (type)/(name) -c (container-name)`
- kubectl attach deployment/nginx-deploymnent -c nginx
- 현재 실행중ㅇ니 컨테이너 프로세스에 접속하여 로그 확인

`kubectl logs (type)/(name) -c (container-name) -f`
- kubectl logs deployment/nginx-deployment -c nginx -f
- 현재 실행중인 컨테이너 프로세스에 모든 로그 출력 (-f: watch 모드)

