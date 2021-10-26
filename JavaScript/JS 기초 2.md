## 함수(function)

서비스를 만들다 보면 작거나 비슷한 동작들이 생기기 마련. 재활용하는게 편하겠죠? 함수는 이걸 가능하게 해줍니다. 
우리는 저번 시간에 브라우저가 가지고 있는 내장함수인 `console`, `alert`, `confirm` 등을 써봤어요.

함수는 이렇게 작성합니다.
```
    function sayHello(name){
        console.log(`Hello, ${name}`);
    }
```

sayHello("MIKE"); // 이런식으로 호출이 가능합니다.

c나 자바나 이런데에서 썼던거 마냥 잘 쓰시면됩니다.

```
    function sayHello(name){
        let newName = name || 'friend';
        let msg = `Hello, ${newName}`
        console.log(msg)
    }

    sayHello(); //Hello Friend 출력 _ or 박았을때 맨 뒤에께 출력되는듯
    sayHello('Jane'); // Hello Jane 출력
```

반환하는것도 알아봅시다

```
    function add(num1, num2){
        return num1+num2;
    }

    const result = add(2,3);
    console.log(result); //이럼 5가 찍혀요
```
