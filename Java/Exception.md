# 예외 및 예외처리 방법

## 예외
### 의미?
- 에러(error): 개발자가 해결할 수 없는 치명적인 오류
- 예외(exception): 개발자가 해결할 수 있는 오류
- 예외가 발생하면 비정상적인 종료를 막고 프로그램을 계속 진행할 수 있도록 우회경로를 제공하는 것이 바람직.

### 종류
- 일반 예외(검사형 예외), 실행 예외(비검사형 예외)

### 실행 예외
- 예외가 발생하면 JVM은 해당하는 실행 예외 객체를 생성
- 실행 예외는 컴파일러가 예외 처리 여부를 확인하지 않음. 따라서 개발자가 예외 코드의 추가 여부를 결정.

#### 대표적인 실행 예외
- ArithmeticException : 0으로 나누기와 같은 부적절한 산술 연산을 수행할 때 발생한다.
- IllegalArgumentException : 메서드에 부적절한 인수를 전달할 떄 발생한다.
- IndexOutOfBoundsException : 배열, 벡터 등에서 범위를 벗어난 인덱스를 사용할 때 발생한다.
- NoSuchElementException : 요구한 원소가 없을 때 발생한다.
- NullPointException : null 값을 가진 참조 변수에 접근할 때 발생한다.
- NumberFormatException : 숫자로 바꿀 수 없는 문자열을 숫자로 변환하려 할 때 발생한다.

### 일반 예외
- 컴파일러는 발생할 가능성을 발견하면 컴파일 오류를 발생
- 개발자는 예외 처리 코드를 반드시 추가

#### 대표적인 일반 예외 예
- ClassNotFoundException : 존재하지 않는 클래스를 사용하려고 할 떄 발생한다.
- InterruptedExceptin : 인터럽트되었을 때 발생한다.
- NoSuchFieldException : 클래스가 명시한 필드를 포하하지 않을 때 발생한다.
- NoSuchMethodException : 클래스가 명시한 메서드를 포함하지 않을 때 발생한다.
- IOException : 데이터 읽기 같은 입출력 문제가 있을 때 발생한다.

## 예외 처리 방법
- 예외 잡아 처리하기
- 예외 떠넘기기

### 예외 잡아 처리하기
- 일반적인 코드 : 에외가 발생하면 오류 발생으로 프로그램 종료
- try ~catch 코드 : 예외가 발생하면 그 오류를 catch 해서 핸들러 안에서 처리

```
try{
  //예외 발생
  //예외가 발생하면 예외 객체를 catch 블록의 참조 변ㅅ로 전달한다.
}catch (예외 클래스1 참조변수){
  핸들러;
}catch(예외 클래스2 참조변수){
  핸들러;
}

```
```
try{
  예외가 발생할 수 있는 실행문;
} catch (예외 클래스1 | 예외 클래스2 변수){ //다수의 예외를 한꺼번에 잡으려면 | 연산자로 연결하면된다.
  핸들러;
}
```

#### Throwable 클래스의 주요 메서드
public String ageMessage() : Throwable 객체의 자세한 메시지를 반환한다.
public String toStirng() : Throwable 객체의 간단한 메시지를 반환한다.
public void printStackTrace() : Throwable 객체와 추적 정보를 콘솔 뷰에 출력한다.

#### try~with~resource문
- try 블록에서 파일 등과 같은 리소스를 사용한다면 try 블록을 실행한 후 자원 반환 필요
- 리소스를 관리하는 코드를 추가하면 가독성도 떨어지고, 개발자도 번거롭다.
- JDK 7부터는 예외 발생 여부와 상관없이 사용한 리소르를 자동 반납하는 수단 제공, 단, 리소스는 AutoCloseable의 구현 객체

```
try(리소스)
{
}catch(...
){
}
```
- JDK 7과 8에서는 try()의 괄호 내부에서 자원 선언 필요.
- JDK 9부터는 try 블록 이전에 자원 선언 가능. 단, 선언된 자원 변수는 사실상 final이어야 함.

```
try(PrintWriter out = new PrintWriter("a.txt"))
{
}catch(...){
}
```
```
PrintWriter out = new
PrintWriter("a.txt");
try(out){
} catch(...){
}
```

### 예외 떠넘기기
- 메서드에서 발생한 예외를 내부에서 처리하기가 부담스러울 때는 throws 키워드를 사용해 예외를 상위 코드 블록으로 양도 가능.
- 예외를 생성한 메서드 => throws => throws => throws=> 예외를 처리하는 메서드 => 처리

#### 사용 방법
```
public void write(String filename)
  throws IOEception, ReflectiveOperationException {
  //파일쓰기와 관련된 실행문...
}
```
- 자바 API 문서를 보면 많은 메서드가 예외를 발생시키고 상위 코드로 예외 처리를 떠넘긴다. 예를 들면

```
public static void sleep(long milis, int nanos) throws InterruptedException
```

이런식으로 말이다.



