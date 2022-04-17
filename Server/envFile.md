# .env 파일에서 민감한 환경변수 설정하기 
## 강의를 들으며 작성했던 코드를 한번 살펴보자.
```js
var db;
MongoClient.connect('mongodb+srv://codingapple1:어쩌구@저쩌구', function(err, client){
  if (err) return console.log(err)
  db = client.db('Example1');
  app.listen(8080, function() {
    console.log('listening on 8080')
  })
}) 
```
- 다른 컴퓨터에서 다른 포트를 연다던지
- db 이사를 간다던지
- 내가 만든 코드를 팀원과 공유해야하는데 내 아이디 비번이 적혀있으면 조금 그렇잖슴?

> 이런 환경에 따라 바뀌는 변수데이터들을 보통 <b>환경변수 </b> 라고 부름.

- 그래서 개발자들은 .env 이라는 파일에 환경변수들을 떄려박음.
- 그리고 server.js 에 가서 "env 파일에 있는 포트 숫자 여기에 넣어주세요 ~ " 라는 식으로 코딩 
- server.js 가 털려도 중요한건 env 파일에 있기 떄문에 보안상 조금의 이점도 있음.

## 사용과정
### 1. 환경변수 사용을 위한 라이브러리를 설치한다. 
- `npm install dotenv` 라고 입력해줍시다

### 2. 환경변수가 있는 server.js에 방금 설치한 라이브러리 등록합니다.
```js
(server.js)

require('dotenv).config()
```

### 3. server.js와 같은 경로에 .env 파일을 하나 만들어줍니다.
- 그리고 나중에 변경이 될 것 같은 환경변수들을 다 적어줍니다.
- 형식은 var 문법으로 숫자,문자 변수 만드는거랑 똑같이 왼쪽 : 변수명, 오른쪽 : 값
- 변수 이름들은 <b>대문자</b>로
- 나중에 작업환경이 바뀌거나 클라우드에 올릴 때도 이것만 변경해주면 쉽게 환경셋팅이 가능해짐
```js
(.env)

PORT=8080
DB_URL="mongodb+srv://codingapple1@저쩌구"
```

### 4. 환경변수들을 불러와봅시다.
- `mongodb+srv://어쩌고` -> `process.env.DB_URL` 이런 식으로

## 마치며
- 나중에 클라우드 서비스를 이용해서 서버를 발행할때도 env 파일을 똑같이 이용가능.
- env 를 따로 만드는게 아니라 뭐 다른 작업을 해야되긴하는데 알잘딱 가이드들 참고해서 해봅시다. 와!



 