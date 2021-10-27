## 함수
- 한번에 한작업에 집중 
- 읽기 쉽고 어떤 동작인지 알 수 있게 네이밍

## 함수 표현식 화살표 함수

``` 
    function sayHello(){
        console.log('Hello);
    }

    // 요건 함수 선언문

    let sayHello = function(){
        console.log('Hello');
    }

    // 요건 함수 표현식

    // 선언문이랑 표현식이랑 다른게 거의 없어용.
    // 다만 함수 선언문은 어디서든 꺼내다 쓸 수 있고
    // 표현식은 호출하는게 위에 있으면 쓸 수 없어요.

```

이제 화살표 함수도 알아봅시다.

```
    let add = function(num1,num2){
        return num1+num2;
    }

    //를 화살표 함수로 바꿔봅시다.

    let add = (num1,num2) =>(
        num1+num2'
    )

    //훨씬 간단하죠?


```

## 객체

```
    //요게 객체에요
    const superman = {
        name : 'clark';
        age: 33,
    }

    //접근을 하고 싶으면
    superman.name //'clark'
    superman['ago] // 33

    //추가
    superman.gender = 'male';
    superman['haircolor'] = 'black';

    //삭제
    delete superman.hairColor;

    //단축 프로퍼티

    const name = 'clark';
    const age = 33;

    const supermain = {
        name, // name : name,
        age,  // age : age,
        gender : 'male',

        //처럼 사용 가능합니다.
    }

    ///for..in 반복문

    for(let key in superman){
        console.log(key)
        console.log(superman[key])
    }

    //예제

    const Mike = {
        name = "Mike",
        age:30
    };

    for(x in Mike){
        console.log(Mike[x])
    }






```