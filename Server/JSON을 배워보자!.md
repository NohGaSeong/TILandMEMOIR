# JSON 에 대해 여러가지를 알아보자
## JSON 이란?
- JavaScripts Object Notation
- 경량의 DATA 교환 형식이다.
- 속성-값 쌍 || 키-값 쌍으로 이루어진 데이터 오브젝트를 전달하기 위해 인간이 읽을 수 있는 텍스트를 사용하는 개방형 표준 '포맷'
- 쉽게 말하면 데이터 주고 받을 때 트래픽을 최소화하기 위한 데이터가 들어있는 가벼운 종이
- 시작은 JS But 언어 독립형 포맷. (수년간 지배 해왔던 XML을 대체 할 수 있는 주요 데이터 포맷)
- ajax 등을 사용했을때 JSON 형식으로 받았었는데 그 JSON 이 맞다
- 프로그램 언어의 제약이 거의 없으며 C,JAVA,Ruby 드 거의 모든 언어에서 사용 가능하다.

## JSON 문법의 종류
- Number : number은 8진수와 16진수 현식을 사용하지 않은 것을 제외하면 C의 Number과 비슷하다
- String : 0개 이상의 유니코드 문자들의 연속. 문자열은 큰 따옴표(")로 구분하여 역슬래시 이스케이프 문법을 지원
- True/False : 값
- Array : 리스트. 대괄호로 다타내며 요소는 쉼표로 구분
- Object : 순서가 없는 이름/값 쌍의 집합, 이름(키) 문자열
- NULL : 빈 값

## JSON의 사용 이유?
- 사람 기계 둘 다 이해하기 쉬우며 용량이 적음.
- 특정 언어에 종속되지 않고 대부분의 프로그래밍 언어에서 사용 가능함
- <b>제일 중요한 사용 이유는 데이터를 전송할 때 최소한의 용량으로 전송하기 위함임.</b>
- AJAX 와 REST API 통신 할 때 자주 받는 데이터 형식인 만큼 필수적으로 알아두어야한다.

## JSON 예제를 따라하며 문법을 익혀보자
### key:value 형식
```.json
{
  "key":"value",
  "key":"value",
  "key":"value"
}
```

## JS 에서 JSON 데이터 뽑기, 추출하기
### JSON 형태 데이터
```.json
var param1= {
  "fruit": "Apple",
  "size": "Large",
  "color": "Red"
}
```
### JS
```.js
$(document).ready(function(){

jsonTest();

})

function jsonTest(){
  console.log(param1.fruit);
  console.log(param1.color);
}
```

### 결과
Apple
Red

### 내가 이해한대로 설명해보자
- JSON 형식 데이터를 param1 이란 변수에 담고 param1의 fruit 이란 key 의 값을 콘솔로 찍겠다는 뜻.
- 아래는 color . 따라서 fruit의 value와 color의 value 인 apple 과 red 가 console.log 에 찍힌다.

## 조금 복잡한 예제
### JSON
```.json
var param2 = {
    "quiz": {
        "sport": {
            "q1": {
                "question": "Which one is correct team name in NBA?",
                "options": [
                    "New York Bulls",
                    "Los Angeles Kings",
                    "Golden State Warriros",
                    "Huston Rocket"
                ],
                "answer": "Huston Rocket"
            }
        },
        "maths": {
            "q1": {
                "question": "5 + 7 = ?",
                "options": [
                    "10",
                    "11",
                    "12",
                    "13"
                ],
                "answer": "12"
            },
            "q2": {
                "question": "12 - 8 = ?",
                "options": [
                    "1",
                    "2",
                    "3",
                    "4"
                ],
                "answer": "4"
            }
        }
    }
}
```
### JS
```.js
$(document).ready(function(){
jsonTest();
})

function jsonTest(){
console.log(param2.quiz["sport"].q1.question);
console.log(param2.quiz["sport"].q1.options[2]);
console.log(param2.quiz["sport"].q1.answer);

console.log(param2.quiz["maths"].q1.question);
console.log(param2.quiz["maths"].q2.question);
}
```
### 결과
Which one is correct team name in NBA?
Golden State Warriros
Huston Rocket
5 + 7 = ?
12 - 8 = ?

### 내가 이해한대로 적기
- param2 라는 변수의 quiz 아래의 ["sport"] 의 아래의 q1 의 question
- 이런식으로 생각하면 편할 듯 싶다.
- sport 를 왜 [] 안에 넣었는지 의문이 든다. 애들한테 물어보고 추가적으로 적어야겠다.

(조금 이따 적을 예정)


