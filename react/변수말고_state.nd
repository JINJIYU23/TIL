# 변수 말고 State

- 리액트에서는 변수 말고 state를 이용하여 데이터를 저장할 수 있음

```jsx
import { useState } from 'react';
import './App.css'

function App(){
 
  let [a,b] = useState('남자 코트 추천');  
  // 보관할 자료, a : 남자코트추천(자료가 들어있음) b : state변경을 도와주는 함수
  let posts = '강남 우동 맛집';
  return (
    <div className="App">
      <div className="black-nav">
        <div>개발 blog</div>
      </div>
      <div className="list">
        <h4>글제목</h4>
        <p>2월 17일 발행</p>
        <hr/>
      </div>
    </div>
  )
}
```

let [a,b] → **JS destructuring**

array안에 있는 데이터들을 변수로 쉽게 저장하는 문법

state는 변수와 같은 용도이지만, 변동 사항이 생기면 state를 쓰는 html도 자동 랜더링

따라서 자주 변하는 데이터들을 저장하는데 용이

이게 되나..? 라고 생각했던게 되는걸 보고 신기하단 생각이 들었움,,