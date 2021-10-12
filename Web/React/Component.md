# React의 컴포넌트란?

## 컴포넌트란?
`컴포넌트는 데이터를 입력받아 DOM Node를 출력하는 함수이며앱을 이루는 최소한의 단위이다. `

이때 입력받는 데이터는 props나 state 같은것들이 있다.

## 그럼 이 Props나 State는 뭘까?

### props
부모 컴포넌트가 자식 컴포넌트에게 주는 값이다. 어떠한 값을 컴포넌트에 전달해 줘야 할 때 사용하며 할당된 후 컴포넌트 내부에서 값을 변경 할 수 있다.

### State
컴포넌트 내부에서 선언하며 내부에서 값을 변경할 수 있다. 동적인 데이터를 다룰땐 state를 사용한다. 

### 따라서
컴포넌트 간에는 props를 통해 데이터를 주고 받고 , 변경되는 값은 state 만큼만 확인하면된다.

## 자주 사용되는 함수들

### render()
- 클래스형 컴포넌트에서 반드시 구현해야하는 유일한 메서드이다. props와 state 값을 활용하여 값을 반환한다.

- 컴포넌트의 state를 변경하지 않고, 호출될 때마다 동일한 결과를 반환해야한다.

### constructor(props)
- 메서드를 바인딩하거나 state를 초기화하는 작업에서 사용된다.
### componentDidMount()
- 컴포넌트가 마운트된 직후 호출된다.
- DOM 노드가 필요한 초기화 작업을 수행한다.
### componentDidUpdate(precProps, prevState, snapshot)
- 갱신이 일어난 직후 호출되며 최초 렌더링에서는 호출되지 않는다.
- 컴포넌트 갱신시 DOOM을 조작할때 사용한다.
### componentWillUnmount()  
- 컴포넌트가 마운트 해제되어 제거되기 직전에 호출된다. 

## 컴포넌트의 종류
### 1.함수형 컴포넌트
`function WebApp(props){
    return <h3>Name is {props.name}</h3>;
}
`<br>
데이터를 가진 props 객체 한개를 받고 React 엘리먼트를 반환.
JS 함수 ==> `함수형 컴포넌트`

### 2.클래스형 컴포넌트
`class WebApp extends React.Component{
    render(){
        return <h3>Name is {this.props.name}</h3>;
    }
}` <br>
함수형 컴포넌트로 하지 못하는 작업을 처리할 때 ES6 class를 사용한 `클래스형 컴포넌트`를 활용한다.

## 마치며
학교 인터넷으로 도대체 왜 리엑트 공식문서에 들어가지지 않는지.. 참.. 

## 참조
<a href = "https://reactjs-kr.firebaseapp.com/docs/state-and-lifecycle.html">React 공식문서</a><br>
<a href = "https://velog.io/@jgam/%EB%A6%AC%EC%95%A1%ED%8A%B8%EC%9D%98-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8%EB%9E%80">리액트의 컴포넌트란...?</a><br>
<a href = "https://medium.com/little-big-programming/react%EC%9D%98-%EA%B8%B0%EB%B3%B8-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8%EB%A5%BC-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90-92c923011818">React의 기본, 컴포넌트를 알아보자</a><br>
