# useEffect

컨포넌트는 

1. mount : 페이지에 장착
2. update : 업데이트
3. unmount : 필요 없으면 제거

**useEffect**를 사용하면, 

각각의 실행할 코드를 입력할 수 있다. (페이지 장착 시, 업데이트 시, 제거 시 이거 해줘~~~)

```jsx
import {useState, useEffect} from 'react';

function Detail(){

  useEffect(()=>{
    //여기적은 코드는 컴포넌트 로드 & 업데이트 마다 실행됨
    console.log('안녕')
  });

  let [count, setCount] = useState(0)
  
  return (
    <button onClick={()=>{ setCount(count+1) }}>버튼</button>
  )
}
```

버튼을 누를 때 마다, console.log(’안녕’) 실행.

대신 **useEffect 안에 적은 코드는 html 렌더링 이후에 동작. (오래 걸리는 반복연산, 서버에서 데이터 가져오는 작업, 타이머 다는거…. )**

---

2초 후 박스가 없어지는 기능을 이제 useEffect를 이용해서 만들건데, 이거 만들때 동적인 UI를 만드는 법을 까먹어서 다시 찾아봤다. 

```jsx
function Detail(props) {

   2초 후 창 사라지기
   useEffect(() => {
     setTimeout(() => {setAlert(false)}, 2000);
   }, [])

  2초 후 창 사라지기
  let[alert, setAlert] = useState(true);

    return (
      <div className="container">
        {
          alert === true ? <Alert></Alert> : null
        } 
      </div> 
    )
}

// 2초 후 박스 없애기
function Alert() {
  return (
    <div className="alert alert-warning">
      2초이내 구매시 할인
    </div>
  )
}
export default App;
```

내가 짠 코드는 살짝 더러운 느낌이 드는데 뭔가 그래도 나쁘지 않은 듯.

근데, 이제 처음에 짰을 때는 약간 갑자기 2초마다 사라지고 다시 생기고 이게 반복 되었었다.

원인을 알고보니  맨 마지막 [] 이것이 없어서였다. 

```jsx
  useEffect(() => {
     setTimeout(() => {setAlert(false)}, 2000);
   }, [])
```

---

이젠, useEffect에 넣을 수 있는 실행 조건에 대해 알아보자.

`useEffect(()=>{ 실행할코드 })`  : 재렌더링마다 코드를 실행

`useEffect(()=>{ 실행할코드 }, [])`  : 컴포넌트 mount(로드 시) 1회만 실행 가능

```jsx
useEffect(()=>{
return ()=>{
실행할코드
}
})
```

: useEffect 안의 코드 실행 전에 항상 실행

```jsx
useEffect(()=>{ 
  return ()=>{
    실행할코드
  }
}, [])
```

: 컴토넌트 unmount 시, 1회만 실행

```jsx
useEffect(()=>{
실행할코드
}, [state1])
```

: state1 이 변경될 때만 실행

---

<input> 에 입력한 값이 숫자가 아니면 alert박스 띄우기

```jsx
function Detail(props) {

  // 검색창에 숫자 외 입력하면 경고창 띄우기
  let[num, setNum] = useState('');

  // 검색창에 숫자 외 입력하면 경고창 띄우기
  useEffect(() => {
    if (isNaN(num) === true) {
      alert('숫자가 아닙니다.');
    }
  }, [num])

    return (
      <div className="container">
        <div className="row">
          <div className="col-md-6">
            <img src="https://codingapple1.github.io/shop/shoes1.jpg" width="100%" alt=''/>
          </div>
          <div className="col-md-6">
            {/* // 검색창에 숫자 외 입력하면 경고창 띄우기 */}
            <input onChange = {(e) => {setNum(e.target.value)}}></input>
            <h4 className="pt-5">{idid.title}</h4>
            <p>{idid.content}</p>
            <p>{idid.price}원</p>
            <button className="btn btn-danger">주문하기</button> 
          </div>
        </div>
      </div> 
    )
}
```

isNaN(’’)의 안에 값이 숫자면 false

isNaN(’’)의 안에 값이 숫자가 아니면 true

일단, onChange안에 함수를 쓸 수 있다는 걸 까먹었었다. (일단은 onchange도 기억 안남..)

또, 자꾸 망각하는게, useState의 사용에 대해 망각한다.

뭔가 자꾸 새로운 상황에 대해 변화를 시키려면 useState에 대한 내용을 잘 알아야 될 것 같다.