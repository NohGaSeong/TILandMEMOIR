# Mr.blog 를 만들면서 느낀 소감과 이 토이 프로젝트? 로 배운것

## 배운걸 적기 앞서
진짜 어려웠어요. 리엑트로 만들라고하면 만들만했을 것 같은데 순수 바닐라 js 만 사용해서 만들라고하니 어질어질했고 그 덕에 친구들한테도 엄청 물어보고 친구들과 선배들의 코드를 많이 참고했던 것 같아요. 하지만 이런 짓을 한 덕에 js 실력이 단기간에 진짜 늘어난 것 같아요. 여기선 이 프로젝트를 어떻게 했는가에 대해 적기보단 이 프로젝트로 배운 부분들을 기록할려고해요.

## fetch
`fetch 란? : api를 불러오고, 정보를 내보내주는 함수에요.`

json 파일안에 담겨 있는 질문들을 받아오기위해 사용한 함수인데 사용법은 아래와 같아요.
```
  fetch(url, options)
  .then((response) => console.log("response:", response))
  .catch((error) => console.log("error:", error));
```
함수는 첫번째 인자로 URL, 두번째 인자로 옵션 객체를 받고, Promise 타입의 객체를 반환해준다고해요. 
반환된 객체는 API 호출이 성공했을 경우에는 응답(response) 객체를 resolve하고, 
실패했을 경우에는 예외(error) 객체를 reject한다고하네요.

## await / async
비동기 코드를 동기적인 코드로 작성할 수 있게 해주는 문법이에요. 이 프로젝트에선

```
  async function printDate(i) {
    let questions;
    await fetch("./db/data.json") 
        .then((response) => response.json())
        .then((datas) => (questions = datas.questions));
  
    const month = questions[i].id[0] + questions[i].id[1];
    const day = questions[i].id[2] + questions[i].id[3];
    const question = questions[i].question;
    
    document.getElementById('month').innerHTML = month;
    document.getElementById('day').innerHTML = day;
    document.getElementById('question').innerHTML = question;
    answer.value = getAnswer(i);
  }
```

이런식으로 작성했어요. async 는 함수 앞에 위치하고 async를 붙힌 함수는 promise 를 반환해줘요. await 를 만난 promise 는 비동기 처리가 될 때까지 기다리다 반환해줘요. await 는 무조건
비동기 처리한 프로미스 앞에 적어줘야한다고해요.

## getElementbyId
태그에 있는 id 속성을 사용하여 해당 태그에 접근하여 하고 싶은 작업을 할 때 쓰는 함수에요.
해당 id가 없는 경우 null 에러가 발생하기에 ID가 없는 요소에 접근하려면 document.querySelector()를 사용해야된다고해요.

```
  let nextBtn = document.getElementById('next-btn');
  let prevBtn = document.getElementById('prev-btn');
  let saveBtn = document.getElementById('save-btn');
  let answer = document.getElementById('answer-input');
```

이런식으로 버튼이나 어떤걸 넣어줘야되는 부분의 id를 가져왔어요

## addEventListener
addEventListener()는 document의 특정요소(Id,class,tag 등등..) event(ex - click하면 함수를 실행하라, 마우스를 올리면 함수를 실행하라 등등.. )를 등록할 때 사용해요.
이 프로젝트에선 click 하면 handle~ 함수를 실행해라! 라는 식으로 사용했어요.

```
  document.getElementById('next-btn').addEventListener('click', handleNext);
  document.getElementById('prev-btn').addEventListener('click', handlePrev);
  document.getElementById('save-btn').addEventListener('click', handleSave);
```

## getDate
new Date() 함수는 함수가 실행되는 시점에 날짜 및 시간 데이터를 갖고 오는 함수에요. 출력하게 되면 요일, 월, 일, 연, 시, 분, 초 GMT기준시간을 표시해요.

```
  let current = new Date();
  let date = current.getDate(); // 오늘 날짜가져오기
```

이런식으로 요일을 가져오는데 사용하였어요.

## local storage
일정 시간 또는 영구적으로 값을 저장하고 싶은 경우에 사용할 수 있는 것이 WebStorage API인 로컬 스토리지(LocalStorage)에요.

```
・데이터를 사용자 로컬에 보존하는 방식.

・데이터를 저장, 덮어쓰기, 삭제 등 조작 가능.

・자바스크립트(JavaScript)로 조작.

・모바일에서도 사용 가능
``` 
이런게 가능하다고해요.

사용방법은 
```
/**
 * 로컬 스토리지에서 데이터를 가져오는 함수
 *
 * @ param {string} key: 데이터의 키
 * @ return {string} 해당 키에 대한 데이터
 */
export function getAnswer(key) {
    let value = localStorage.getItem(key);
    return value;
}

/**
 * 로컬 스토리지에 데이터를 저장하는 함수
 *
 * @ param {string} key: 저장할 데이터의 키
 * @ param {string} value: 저장할 데이터
 */
export function setAnswer(key, value) {
    localStorage.setItem(key,value);
}
```

이런식으로 받아오고 , 보내줄 key와 value를 js 에서 보내주면돼요.

## 느낀점
다음에는 또 다른걸 만들텐데 잘할 수 있을지 모르겠네요..ㅠ


