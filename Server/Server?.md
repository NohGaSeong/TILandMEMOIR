# 서버란?

## 사전적 의미
- 클라이언트에게 네트워크를 통해 정보나 서비스를 전달하는 컴퓨터
- 클라이언트 요청에 의해 어쩌고 저저고

## 이해하기 쉽게 인간의 언어로 알아보자
`서버 == 닭갈비집 알바생` 이라고 볼 수  있어요. 우리가 닭갈비 집에 들어가서 "닭갈비 2인분 주세용" 하면 알바생이 닭갈비 2인분을 서빙해주죠? 그거랑 똑같애요.

서버 : 요구를 하면 가져다줌. (스테이크를 요청하면 스테이크를, 저거를 요청하면 저거를 그대로 가져다주고. )

네이버웹툰에 만화페이지를 요청하면서 만화 버튼을 누르면 만화페이지가 뜨고, 웹소설 페이지를 요청하면서 웹소설 버튼을 누르면 웹소설 페이지를 요청하면 웹소서 페이지를 가져다주고. 그런식인거죠.

서버는 별거 없어요! `요청을 받으면 요청한 내용을 보내주는 프로그램` 이에요. 별로 어려운걸 하는게 아니에요.

서버: 닭갈비집 알바생
서버개발자: 닭갈비집 알바생 메이커

이제 코드를 어떤식으로 작성하는지 인간의 언어(한글)로 적어볼게요.

```
    어떤 사람이 comic.naver.com 으로 접속하면
    네이버웹툰 메인 html 파일을 전송해주세요
```

다시한번 정리를 해볼게요

`서버: 요청(HTTP 요청)을 받으면 요청한 내용을 보내주는 프로그램`

## HTTP의 4가지 요청
1. 읽기
2. 쓰기
3. 수정
4. 삭제

### 읽기(GET)
- 나 이런 페이지 읽고싶어! 라는 요청 기능

### 쓰기(POST)
- 댓글 작성, 블로그 포스트 작성 등을 할때 쓰는 기능
- "이거 글 좀 올려주세용 ~ "

### 수정(PUT)
- 뭔가 수정할 때
### 삭제(DELETE)
- 뭔가 삭제할 때

최종 정리!
`서버: 요청(사용자는 GET/POST/PUT/DELETE 요청 가능)을 받으면 요청한 내용을 보내주는 프로그램`

그래서 앞으로 어떤 코드를 짜게 될까요?

```
    어떤 사람이 /list 라는 페이지를 GET요청하면 ...
    거기 해당하는 list.html 파일을 보내줌

    //이럼 멋진 서버 개발 끝!
    //이걸 Node.js 를 이용해서 JavaScript문법으로 서버를 짤거에요!
```
