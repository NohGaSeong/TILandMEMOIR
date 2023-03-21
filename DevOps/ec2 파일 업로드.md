## EC2에 파일 업로드
### 무슨 이유로 파일 업로드?
분명 보안을 이유로 bastion 을 거쳐서 private ec2든 ecs든 통신, 접속이 가능할 것이다. 그러기 위해선 private ec2의 pem 키를 bastion 으로 업로드해야하는데 필자가 선호하는 방법을 적어본다.

### pem키 업로드 : vi .pem , 컨트롤 c 컨트롤 v
필자가 1학년부터 이용하던 방법이다.

1. 접속해야하는 private ec2를 한번 확인해준다.
![](https://velog.velcdn.com/images/noyohanx/post/057d59c3-d5ac-4343-8464-b97e0830f07e/image.png)
2. 이후 bastion 인스턴스에 접속
![](https://velog.velcdn.com/images/noyohanx/post/d1714594-6d95-4898-9e03-83d8861a7c6b/image.png)ㅓ
3. 다음 private ec2의 pem 키가 있는 경로로 이동후 pem 키를 텍스트 편집기 및 메모장으로 열어준다. 그러면 `-----BEGIN RSA PRIVATE KEY-----` 로 시작해서 `-----END RSA PRIVATE KEY-----` 로 끝나는 텍스트들이 나오는데 컨트롤 A, 컨트롤 C 해준다. (전체 선택, 복사)
![](https://velog.velcdn.com/images/noyohanx/post/c2c055cb-8397-4226-8879-11ed76b966eb/image.png)
이후 bastion 인스턴스에 들어와 vi (pem key 이름).pem 으로 파일을 생성하고 붙여넣기, 이후 :wq! 를 입력해준다. (:wq! = 저장하고 vi 라는 편집기를 종료한다는 뜻이다.)
![](https://velog.velcdn.com/images/noyohanx/post/b19b1d72-fb8d-46bf-85e8-38a8f07a48df/image.png)
5. 4번의 과정을 끝냈다면 이렇게 pem 키가 잘 생성되었을것이다. 이후 이 pem 키를 이용하여 privaet ec2에 접속해주자.
![](https://velog.velcdn.com/images/noyohanx/post/cdb2e51f-ef89-4466-93f4-48e83f81d5c6/image.png)
5. 짠. 1번 과정에서 확인했던 private ec2의 ip 로 잘 접속한 것을 볼 수 있다.
![](https://velog.velcdn.com/images/noyohanx/post/33cfeb74-192d-454c-8017-e18d9355fd9c/image.png)

### Flask 앱 업로드
필자의 예상으론 public ec2 가 과제 public subnet에 있는데 bastion 의 역할 or flask 파일을 ecr 쪽으로 업로드 하는 역할을 수행할 수도 있으므로 ec2에 앱을 업로드하는 방법을 알려주겠다.

... 어 그냥 컨트롤 c 컨트롤 v 하고 필자의 [이 글](https://velog.io/@noyohanx/2023-%EC%A7%80%EB%B0%A9%EB%8C%80%ED%9A%8C-%EC%A4%80%EB%B9%84-1.-Flask)과 똑같이 하는게 더 빠를 듯 싶다. 오류가 뜬다면 구글링을해서 빨리 고치고. 어차피 깃허브에 올려서 크론을 받나 뭘 하나 컨c컨v 한 파일이랑 똑같은 작업을 진행해야한다. 파일이 많지도 않으니 그냥 긁어서 세팅만 해주자.
