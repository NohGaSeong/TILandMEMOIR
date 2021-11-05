# 메소드를 알아봅시다.

## 메소드?
자바에서 클래스는 멤버로 속성을 표현하는 필드와 기능을 표현하는 메소드를 가집니다.
그 중에서 메소드란 어떠한 특정 작업을 수행하기 위한 명령문의 집합이라 할 수 있습니다. 

## 메소드 사용목적
- 반복적인 프로그래밍을 피할 수 있기 때문
- 모듈화로 인해 코드의 가독성이 좋아짐
- 유지보수 편하게 가능

## 메소드 정의
함수랑 다를바가 없습니다.

```
  접근제어자 반환타입 메소드이름(매개변수목록) { //선언부
  //구현부
  }
```

- 접근제어자 : 해당 메소드에 접근할 수 있는 범위 명시
- 반환 타입 : 메소드가 모든 작업을 마치고 반환하는 데이터의 타입을 명시합니다.
- 메소드 이름 : 메소드를 호출하기 위한 이름을 명시함
- 매개변수 목록 : 메소드 호출 시에 전달되는 인수의 값을 저장할 변수들을 명시함
- 구현부 : 메소드의 고유 기능을 수행하는 명령문의 집합

## 예제
```
  class car{
    private int currentSpeed;
    private int accelerationTime;
    
    public void accelerate(int speed, int second){
      System.out.println(second + "초간 속도를 시속" + speed + "(으)로 가속함");
    }
  }
```

## 메소드 호출
자바에서 위와 가은 방법으로 정의한 메소드는 멤버 참조 연산자 `.` 을 이용하여 호출할 수 있습니다.

문법
1. 객체참조변수이름.메소드이름(); //매개변수가 없는 메소드의 호출
2. 객체참조변수이름.메소드이름(인수1,인수2...) //매개변수가 있는 메소드의 호출

## 예제
```
  class car{
    private int currentSpeed;
    private int accelerationTime;
    
    public void accelerate(int speed, int second){
      System.out.println(second + "초간 속도를 시속" + speed + "(으)로 가속함");
    }
  }
  
  public class Method01 {
    public static void main(String[] args){
      Car myCar = new Car(); //객체 생성
      myCar.accelerate(60,3); //메소드 호출
   }
```
