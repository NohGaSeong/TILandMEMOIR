# c# 문법 몇 개 정리
## 시작
```cs
using System;
//여기에 사용할 .NET 네임 스페이스를 정의한다.
// 예: 제네릭 컬렉션 -> using System.Collections.Generic;
//      파일 입출력 -> using System.IO;
//      정규표현식 -> using System.Text.RegularExpressions;
namespace MainApp{
    //모든 c# 클래스는 한 네임스페이스 안에 선언한다.
    public class HelloWorld
        {
            // 여기에 멤버 변수, 프로퍼티, 메소드 등을 선언한다.
            static void Main(string[] args){
                Console.WriteLine ("Hello Mono World");
        }
    }
}
```

## 클래스
```cs
// ...
 public partial class PartialClass
 {
     public PartialClass()
     {
         // 생성자
     }

     public void Method1()
     {
         // Method1
     }
 }

 public partial class PartialClass
 {
     public void Method2()
     {
         // Method2
     }

     public void Method3()
     {
         // Method3
     }
 }
 // ...

```
- c# 클래스의 기능은 Java 와 거의 동일. 다만 c# 클래스만의 특징을 따로 서술하자면 다음과 같다.
- 분할 클래스 : java 클래스는 모든 멤버들을 한 파일에 작성해야 한다. 하지만 c# 클래스는 위와 같이 Partial 지시자를 사용하여 여러 파일에 나누어 작성 가능.
- 이렇게하면 나누어 놓은 클래스들이 하나의 클래스로 취급됨.

## this, base
### this
- 정의된 클래스로 생성된 인스턴스 자기 자신을 나타내는 키워드이다.
- 같은 이름의 변수가 메서드 스코프와 클래스 단위 스코프에 정의되어 있을 경우 this 키워드를 통해 접근할 수 있다.
```cs
public class Employee{
    private string company;
    private string name;

    public Employee(string name, string company){
        this.name = name;
        this.company = company;
    }
}
```
- 단순히 Name 으로 접근하려고 name = name 을 하더라도 생성자의 name 파라미터에만 접근이 되기 때문에 원하는 작업을 수행할 수 없다.
- 이 경우에 사용하는 것이 this 키워드 이다. this.name = name 을 하게 되면 클래스의 필드에 생성자의 Name 을 대입하는 정상적인 코드를 만들 수 있다.

### base
- base 키워드의 경우 본인이 상속받고 있는 기본 클래스의 멤버에 접근하는데에 사용되는 키워드이다. 
- 상속을 허용하지 않는 static 클래스에서 base 키워드를 사용할 경우 오류가 발생한다.
```cs
public class Person{
    protected string telephone = "12-5555-6666";
    protected string name = "홍길동";

    public virtual void GetInfo(){
        Console.WriteLine("Name : {0}", name);
        Console.WriteLine("Tel: {0}", telephone);
    }
}
class Employee : Person{
    public string id = "ABC56dkf";
    public override void GetInfo(){
        //본인이 상속받은 클래스에 있는 GetInfo 메소드 호출
        base.GetInfo();
        Console.WriteLine("Employee ID : {0}", id);
    }
}
```
## 생성자
- 객체나 구조체가 생성될때 호출되는 메소드
- 선언 방식에 따라서 다양한 접근자를 가진 생성자를 정의할 수 있음.
- 생성자의 이름은 반드시 해당 객체 또는 구조체의 이름과 같아야함.
### 일반 생성자
- static 생성자를 제외한 나머지 생성자는 new 클래스이름() 으로 접근할 수 있다.
- 단, 생성자 앞에 privat이나 internal 을 붙일 경우 필드 정의와 마찬가지로 엑세스가 제한되게 된다.
```cs
public class TestClass
{
    private TestClass()
    {
        Console.WriteLine("Private Constructor");
    }

    internal TestClass(string message)
    {
        Console.WriteLine("Internal Constructor");
        Console.WriteLine("Message: " + message);
    }
    
    protected TestClass(int count)
    {
        Console.WriteLine("Protected Constructor");
        Console.WriteLine("Count: " + count);
    }

    public TestClass(string message, int count)
    {
        Console.WriteLine("Public Constructor");
        Console.WriteLine("Message: " + message);
        Console.WriteLine("Count: " + count);
    }
}

public class Program
{
    public static void Main()
    {
        var cls1 = new TestClass(); // Private 접근이 안되므로 오류
        var cls2 = new TestClass("test"); // 같은 어셈블리가 아닐 경우 오류
        var cls3 = new TestClass(5); // TestClass 또는 TestClass에서 상속받은 클래스가 아닐 경우 오류
        var cls4 = new TestClass("test", 5); // 모든 곳에서 접근 가능
        TestClass cls5 = new("test", 5); // cls5의 타입을 알 수 있으므로 클래스 이름 생략 가능 (C# 9.0부터 지원)
    }
}
```