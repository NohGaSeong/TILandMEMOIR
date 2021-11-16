# 실습
## AWS 인스턴스 생성
### EC2 인스턴스 생성

1. AWS에 로그인해준다. 이후 리전을 서울로 설정해주세요!
2. 인스턴스 생성을 누르면 아래와 같은 AMI 창이 뜨실텐데 프리티어를 제공해주는 Amazon Linux 를 사용할게요
![2-1번](https://user-images.githubusercontent.com/82383294/141995427-45b6e1e7-a09d-4bcd-ae79-4e7ac5b9d7e3.png)

3. EC2 의 유형은 `t2.micro` 프리티어를 지원해주기에 이걸 사용했어요. (굳이 크게 할 필요도 없고요)
![2-2번](https://user-images.githubusercontent.com/82383294/141995429-24071eb1-6f7b-48f5-8ae9-270a80f1ff4f.png)

4. 스토리지는 딱히 건들게 없기에 기본값으로 놔둬줬어요.
![2-3번](https://user-images.githubusercontent.com/82383294/141995431-aa1a0bc8-ebd5-4da2-addc-f1a0c1931cc9.png)

5. 태그는 Name 태그만 만들게요. 이 인스턴스가 어떤 역할을 하는지 이름을 지어주는거라고 생각하면 편해요.
![2-4번](https://user-images.githubusercontent.com/82383294/141995433-bb7b567b-7ea1-4063-95c5-28326ee3d897.png)

6. 인스턴스에 대한 접근을 제어하기 위한 `보안 그룹` 화면이에요. 보안그룹은 `새 보안 그룹`을 만들어줄게요 

  보통 회사 IP만 지정하는 것이 좋고, 정말 필요한 IP 주소와 포트 번호에 대해서만 접속을 허용하는 것이 중요하다고해요.
  
![2-5번](https://user-images.githubusercontent.com/82383294/141995434-1edd1eaa-74b0-40ae-9dde-9f929aa968a6.png)

이후 다 만드셨으면 `검토 및 시작` 버튼을 눌러 자기가 설정을 잘 했는지 한번 확인을 해주시고 인스턴스를 만들어주세요. 
![2-6 번](https://user-images.githubusercontent.com/82383294/141995435-05b00fac-0a69-4266-922b-310a9ad1c177.png)

7. 키페어도 만들어야하실텐데 이 서버에 접속할 수 있는 <b>열쇠</b> 라고 생각하시면 좋아요. 잃어버리면 다시 다운 받지 못하니까 안전하게 보관해주세요!
![2-7번](https://user-images.githubusercontent.com/82383294/141995436-0c642fe2-ad27-4c4e-b320-da0c526aee26.png)

8. 이제 그렇게 생성을 하고 조금 기다려주시면 이렇게 인스턴스가 만들어져요 와! (짝짝)
![2-8번](https://user-images.githubusercontent.com/82383294/141995390-036fec1f-a3af-4960-a2a3-ead8e4dcf441.png)

이제 저희가 만든 인스턴스를 조금 살펴볼까요? DNS,IP와 관련된 항목을 확인하면 인스턴스에 퍼블릭, 프라이빗 도메인과 IP 주소가 각각 할당됐음을 알 수 있어요. 해당 도메인과 IP를 이용해 이 인스턴스에 접근할 수 있어요.

퍼블릭 도메인과 IP는 별도의 설정을 하지 않는 이상 인스턴스가 꺼질 때 사라지고 다시 켜질 때마다 새로 할당받아요.

중요! : <b>켜져있으면 계속 요금 나가니까 사용안하실때는 인스턴스를 중지하는 습관을 가져주세요!</b>

### EC2 인스턴스 접속
제가 예전에 쓴 
<a href = "https://github.com/NohGaSeong/TIL/blob/main/Cloud/Ec2-Lamp-Elb.md>TIL</a> 을 참고해주세요!
  
### HTTP,HTTPS 도 접근 가능하도록 보안 그룹 추가하기
