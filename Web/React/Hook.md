# React Hooks

## React Hooks 이란?
### 등장배경
리엑트의 컴포넌트는 함수형 컴포넌트와 클래스형 컴포넌트로 나뉘는데요. <br>
기존의 개발방식은 일방적으로 함수형 컴포넌트를 사용하고 , state 등을 사용해야할때만 클래스형 컴포넌트를 사용하는 방식이였는데 
Q :왜 클래스형 컴포넌트를 잘안썼나요 ?<br>
A: 코드가 길고 복잡하며 재사용도 힘들어서요ㅠ <br>

근데 그렇다고 함수형 컴포넌트만 쓰자니 State관리나 Life cycle method는 사용해야겠고 .. 그래서 클래스형 컴포넌트의 복잡하고 , 재사용이 힘든 단점들을 해결하고 함수형 컴포넌트 내에서 작업을 할 수 있게 나온게 `Hook` 입니다!

### 예제
예제 몇가지를 볼게요 ! 

```
import React from 'react';

class App extends React.Component{
    render(){
        return(
            <div style = {{ textAlign: "center"}}>
                <div style = {{fontSize: "100px"}}>0</div>
            </div>
        )
    }
}
``` 
![t1](https://user-images.githubusercontent.com/82383294/137146279-2f225eb1-a373-4450-b53c-4f1084e2bd30.png)

그럼 이런 화면이 뜨는데 숫자를 state로 선언하고 숫자를 증가시키고 다운시키는 버튼을 만들어볼게요.

```
import React from "react";

class App extends React.Component {
  state = {
      number: 0
  };
  render() {
    return (
      <div style={{ "textAlign": "center" }}>
        <div style={{ "fontSize": "100px" }}>{this.state.number}</div>
        <button onClick={this.handleClickIncrement}>더하기</button>
        <button onClick={this.handleClickDecrement}>빼기</button>
      </div>
    );
  }
  handleClickIncrement = () => {
    this.setState(state => ({
      number: state.number + 1
    }));
  };
  handleClickDecrement = () => {
    this.setState(state => ({
      number: state.number - 1
    }));
  };
}

export default App;
```

![t2](https://user-images.githubusercontent.com/82383294/137146286-5faed72e-6968-488e-94d0-db6ee3a02dee.png)
숫자를 다루기 위해 컴포넌트에 state를 선언.
더하고 빼는 함수에 this.setState() 메소드를 사용하였어요.

엄청 길죠? 이제 같은 기능을 react hook 을 사용해서 구현해볼게요!

```
import React, { useState } from "react";

const App = () => {
  const [number, setNumber] = useState(0);
  return (
    <div style={{ textAlign: "center" }}>
      <div style={{ fontSize: "100px" }}>{number}</div>
      <button onClick={() => setNumber(number + 1)}>더하기</button>
      <button onClick={() => setNumber(number - 1)}>빼기</button>
    </div>
  );
};

export default App;
```

코드가 많이 줄었죠?

`useState`은 클래스형 컴포넌트의 `state의 선언`과 관리를 짧고 직관적인 코드로 가능하게 해주는 `hook`입니다.

클래스형 컴포넌트에서 setState를 사용하여 state를 변경할 때에 copy로 항상 새로운 객체를 생성해서 전달해줘야하는 불편함이 있었는데 useState를 사용하여 얻은 함수에서는 원하는 값을 인자로 전달하면돼요. state의 선언과 변경과정이 엄청 간소화되죠? 와!

setState과 같은 hook들을 사용해서 Logic 의 재활용이 가능해요! (클래스형 컴포넌트의 단점 해결!) <br>
useState, useEffect, useReducer 등은 React에 내장되어 있는 hook이에요.

필요한 기능이 있는 hook도 우리가 만들어서 쓸 수 있어요!

## 참고
<a href = "https://reactjs-kr.firebaseapp.com/docs/state-and-lifecycle.html">React 공식문서</a><br>
<a href = "https://codingbroker.tistory.com/29">[react] 예제로 따라하는 리액트 훅(hook) - useState</a><br>
<a href = "https://codingbroker.tistory.com/23">[react] 리액트 훅(react hook)이란? - 클래스형 컴포넌트와 비교</a>