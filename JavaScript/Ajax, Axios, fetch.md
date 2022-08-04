# Ajax, Axios, Fetch 통신의 특징과 각각의 장단점을 알아보자.
## Ajax
### 특징
- Asynchronous JavaScript And XML의 약자.
- 자바스크립트를 이용해 클라이언트와 서버 간에 데이터를 주고받는 비동기 HTTP 통신임.
- XMLHttpRequest(XHR) 객체를 이용해서 전체 페이지가 아닌 필요한 데이터만 불러올 수 있음
### 장점
- JQuery 를 이용해 쉽게 구현 가능함.
- Error, Success, Complete의 상태를 통해 실행 흐름 조절 가능
### 단점
- Jquery를 사용해야 간편하고 호환성이 보장됨
- Promise 기반이 아님
### 예제 코드
```.js
var serverAddress = 'https://localhost:3000';

// jQuery의 .get 메소드 사용
$.ajax({
    url: server_address,
    type: 'GET',
    success: function onData (data) {
        console.log(data);
    },
    error: function onError (error) {
        console.error(error);
    }
});
```
## Axios
### 특징
- axios는 Node.js와 브라우저를 위한 Promise API를 활용하는 HTTP 통신 라이브러리입니다.
- 비동기로 HTTP 통신을 할 수 있으며 return을 promise 객체로 해주기 때문에 response 데이터를 다루기 쉽습니다.

### 장점
- response timeout (fetch에는 없는 기능) 처리 방법이 존재
- Promise 기반으로 만들어졌기 때문에 데이터 다루기 편리
- 브라우저 호환성이 뛰어남

### 단점
- 사용을 위해 모듈 설치 필요

### 예제코드
```.js
axios({
  method: 'post',
  url: 'https://localhost:3000/user',
  data: {
    userName: 'Yohan',
    userId: 'Yohan123'
  }
}).then((response) => console.log(response));
```
## Fetch
### 특징
- ES6부터 들어온 JavaScript 내장 라이브러리입니다.
- Promise 기반으로 만들어졌기 때문에 axios와 마찬가지로 데이터 다루기가 쉬워요.
- 내장 라이브러리라는 장점으로 상당히 편리합니다.
### 장점
- 자바스크립트의 내장 라이브러리 이므로 별도로 import 할 필요가 없음
- Promise 기반으로 만들어졌기 때문에 데이터 다루기 편리
- 내장 라이브러리이기 때문에 업데이트에 따른 에러 방지가 가능
### 단점
- 지원하지 않는 브라우저가 존재 (IE11...)
- 네트워크 에러 발생 시 response timeout이 없어 기다려야 함
- JSON으로 변환해주는 과정 필요
- 상대적으로 axios에 비해 기능이 부족

### 에제코드
```.js
fetch("https://localhost:3000/user/post", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    id: "yohan1234",
    description: "hello my name is yohan",
  }),
}).then((response) => console.log(response));
```
