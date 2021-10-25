# JS 를 빠르게 익혀보자!
    너무 쉬운 기초 설명은 빠르게 뛰고 넘어가겠습니다.
## 1. 변수
- 변수는 어떠한 정보에 이름을 붙혀 저장하고 싶을때 사용합니다.
- `name = "MIKE";` `age = 30;` 이런식으로 말이죠.
- 예약어는 변수의 이름으로 사용이 불가합니다.

alert() : 경고창을 띄우는 함수
console.log : log를 찍는 함수

```
    name = "MIKE";
    age = 30;

    alert(name); //을 찍으면 경고창에 MIKE 라고 나오고
    console.log(age) //를 찍으면 콘솔창에 30 이라고 찍힙니다.
```
근데 저 변수명이 유일하다는 보장이 없어서 저렇게만 쓰면 안되는데 이걸 막기위해 `let` 과 `const` 를 붙혀줍니다.

```
    let name = "MIKE";

    //1000 lines

    let name = "google"; //이러면 오류가 나서 아 다른 name 이 있구나 라는걸 알 수 있습니다.
```
const : 절대로 바뀌지 않는 상수
- 수정이 안돼서 파이 , 최댓값 , 생일 등 안바뀌는 상수들을 입력할때 사용해요.

정리해봅시다
`자바스크립트에서 변수를 선언할 때는,<br>변하지 않는 값은 {const},<br>변할 수 있는 값은 {let} 으로 선언하세요`

### 변수 규칙?
1. 변수는 문자와 숫자, $와 _만 사용
2. 첫글자는 숫자가 될 수 없습니다.
3. 예약어는 사용할 수 없습니다.
4. 가급적 상수는 대문자로 알려주세요
5. 변수명은 읽기 쉽고 이해할 수 있게 선언

## 2. 자료형

### 문자형
```
    const name = "mike"; //문자형 string
    const age = 30;

    const name 1 = "mike";
    const name 2 = 'mike';
    const name 3 = `mike`;

    const message = "I'm a boy. "; //큰 따옴표와 작음 따옴표는 차이가 없지만 작은 따옴표를 쓸 때는 큰 따옴표를 쓴다.
    const message2 = 'I\'m a boy.'; // \를 앞에 넣어주면 특수문자로 취급해줌
    const message3 = `My name is ${name}` // 변수 넣어줄때 사용
    
    console.log(message3); //을 찍어주면 My name is mike 가 출력됨
    
    constmessage4 = `나는 ${30+1}살 입니다.`; //같은것도 가능
```

### 숫자형
```
    const age = 30; //숫자형 Number
    const PI = 3.14;

    //대충 이런 연산들 가능함.
    console.log(1+2);
    console.log(10-7);
    console.log(3*2);
    console.log(6/2);
    console.log(6%4);

```

만약 숫자를 0으로 나누면 어떻게 될까요?
=>`Infinity`. 즉, 무한대라는 값을 얻을 수 있습니다.

또 문자를 숫자로 나누면 어떻게 될까요? (Mike/2)
=> `NaN` = Not a number 이 콘솔에 찍히게됩니다.

### Boolean
```
    const a = true; //참
    const b = false; //거짓
```

### NUll 과 underfined

```
    let age;
    console.log(age); //를 찍으면 {underfined}가 찍힌다. age에 값이 없기 때문이다.

    let user = null; //걍 없다는걸 나타내주는겁니다.
```

### typeof 연산자

```
    const name = "MIKE";

    console.log(typeof 3); //출력: "number"
    console.log(typeof name); //출력: "string"
    console.log(typeof true); //출력: "boolean"
    console.log(typeof "xxx"); //출력: "string"
    console.log(typeof null); //출력: "object" 
    console.log(typeof underfined); //출력: "underfined"

```

아 그리고 문자 + 문자 하면 파이썬 마냥 합쳐져요.

```
    const name = "mike"
    const be = "is";
    const human = "man";

    console.log(name + be + human); // 하면은 "mike is man" 이 찍혀요

    //숫자를 섞어 더할 수 도 있는데 이땐 문자열로 바뀌니까 그것도 생각해주세요.
```
### 대화 상자

alert : 알려줌
prompt : 입력 받음
confirm : 확인 받음 

#### alert
alert() : 사용해본적있죠? 사용자와 상호작용을 한다기보단 일반적으로 통보하는 느낌이에요.
#### prompt

```
    const name = prompt("이름을 입력하세요.");
    alert("환영합니다, " + name + "님");

    //이러면 환영합니다 name(입력한 값) 님이 떠요.
    //다른것과 연계해서 약간 상호작용 하는 느낌.

    prompt('예약일을 입력하세요', '2020-10-'); // , 뒤에 있는건 미리 써놔져 있어서 어떤걸 써야할까 등을 알려줄 수 있음.
```
#### confirm
뭔가 확인받을때 사용받을 수 있어요.

```
const isAdult = confirm("당신은 성인입니까?)";

console.log(isAdult)
//취소 확인 텍스트 박스? 가 뜸.
```

정리를 해봅시다

alert() : 그냥 통보해버립니다.
proppt() : 사용자에게 입력 받습니다.
confirm() : YES NO 를 물어봅니다.

하지만 단점도 있어요.

단점
1. 스크립트 일시 정지
2. 스타일링 x
   
와!

### 형변환
String() -> 문자형으로 변환
Number() -> 숫자형으로 변환
Boolean() -> 불린형으로 변환

#### 왜 필요할까?
prompt 입력 -> 문자형인데 80 90 입력해서 이거 더하면 문자형이라 170이 아니라 8090 이 나와버려요 그래서 이럴때를 대비해서 `형변환`이 필요해요.

### 기본 연산자
'+' : 더하기
'-' : 빼기
'*' : 곱하기
'/' : 나누기
'%' : 나머지

우선 순위 같은건 기본 수학을 아시면 됩니당.

다른 연산자는 c 나 그런 언어랑 똑같아요.

### 비교 연산자, 조건문
'===' : 자료형 , 값이 동일해야함. 강제 형변환 x , == 보다 === 이 좀 더 엄격함.  
나머지는 c랑 똑같음 패스

### 논리연산자

c언어랑 똑같음 . 패스

### 반복문

```
    for(let i = 0; i < 10; i++){
        //반복할 코드
    }

    while(i<10){
        //코드
    }

    do{
        //코드
        //do~while 은 무조건적으로 한번은 실행됨.
        i++
    }while(i<10)

```

### switch

패스
