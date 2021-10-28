## Method, this

### Method
슈퍼맨에게 날라다닌다는 능력을 넣어줘보겠습니다.

```
    const superman = {
        name : 'clark';
        age : 33;
        fly:function(){
            console.log("날아다닙니다.");
        }
    }

    superman.fly(); // 날아다닙니다.
```

<b>method : 객체 프로퍼티로 할당 된 함수<b>

저 fly:function(){} 를 fly(){} 이런식으로 단축해서도 쓸 수 있어요.

```
    const user = {
        name : 'Mike';
        sayHello:function(){
            console.log(`Hello, I'm ${this.name});
        }
        //this == user.sayHello(); ==> Hello, I'm Mike 가 됩니다.
    }
```

자바와 비슷한? 같은? 개념이지만 예제로 좀 더 알아봅시당.

```
    let boy = {
        name : 'Mike';
    }

    let girl = {
        name : 'Jane';
    }

    sayHello:function(){
        console.log(`Hello, I'm ${this.name}`);
    }
```

이 상태에서 sayHello 함수를 각 객체의 메서드로 넣어주도록합시다.

```
    let boy = {
        name : 'Mike';
        sayHello,
    }
```
```
    let girl = {
        name : 'Jane';
        sayHello, 
    }
```

소년과 소녀가 있습니당.

```
    sayHello:function(){
        console.log(`Hello, I'm ${this.name}`); //여기서 this는 아직 정해지지 않았어요.
    }
```

```
    let boy = {
        name : 'Mike';
        sayHello, //각 객체의 메서드로 넣어줍니다.
    }
```
```
    let girl = {
        name : 'Jane';
        sayHello, //각 객체의 메서드로 넣어줍니다.
    }
```
이제 호출을 해봐요

`boy.sayHello();`
`girl.sayHello();`

this는 실행하는 시점에 결정됩니다. sayHello의 this는 . 앞에 있는거에요.

근데 저 함수를 화살표 함수로 지정하면 동작이 완전히 달라지는데 일반 함수와는 다르게 자신만의 this를 가지지 않기 때문이에요.
화살표 함수 내부에서 this를 사용하면 그 this는 외부에서 값을 가져와요.


### this
"자세한건 나중에 알아보겠습니다. 일단은 기초만 알고 있으세요." 라네요

## 배열
뭔 느낌인지 아시죠?

근데 문자,숫자,객체,함수 등을 다 포함 할 수 있어요. 이렇게요

```
    let arr = [
        '민수',
        3,
        false,
        {
            name:'mike',
            age:30,
        },
        function(){
            console.log('Test');
        }
    ];
```

arr.length: 배열의 길이
arr.push() : 배열 끝에 추가.

```
    let days = ['월','화','수'];
    days.push)('목')
    console.log(days //['월','화','수','목'];
```

arr.pop() : 배열 끝 요소 제거
arr.shift() : 배열 앞에 제거
arr.unshift() : 배열 앞에 추가

반복문 : for

```
    let days = ['월','화','수'];

    for(let index = 0; index < days.length; index++){
        console.log(days[index])
    }

```

반복문 : for ~ of

```
    let days = ['월','화','수'];

    for(let day of days){
        console.log(day)
    }
```

## 정리

변수를 만들 수 있고
```
    const name = 'Mike';
    let age = 30;
```
자료형을 이해 가능하며
```
    Boolean
    NULL
    Underfined
    Number
    String
    Object
```
콘솔로 값 확인이 가능하고 사용자들이 원하는 값을 입력받을 수 있습니다.
```
    console.log(name);
    alert(age);
    prompt('생년월일을 입력하세요.');
    confirm('삭제 하시겠습니까?);
```
연산자와 조건문으로 상황 대응이 가능하고
```
    if(user.name && user.age > 19){
        console.log('성입 입니다.');
    }else{
        return false;
    }
```

반복문으로 힘들지 않고 동일한 작업이 가능합니다.
```
    for(let i =0 ; i<10; i++){
        console.log(i);
    }
```
함수와 객체, 배열에 대해서도 알 수 있습니다.
```
    function add(num1,num2){
        console.log(num1+num2);
    }

    const user = {
        name : 'Mike',
        age: 30,
    }

    const users = ['Mike','Jane'];
```

이제 중급에선 좀더 빡씨게 JS를 해봅시다.
