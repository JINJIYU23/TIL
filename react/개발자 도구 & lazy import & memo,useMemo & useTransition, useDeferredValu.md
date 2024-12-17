# 개발자 도구 & lazy import & memo,useMemo & useTransition, useDeferredValue

### 크롬 확장 프로그램 : React Developer Tools

개발 중인 리액트 사이트를 컴포넌트로 미리 볼 수 있음

### profiler 탭을 이용하여 성능 평가 기능

녹화 버튼 누르고 페이지 이동과 버튼 조작을 눌러본 후 녹화를 끝내면 모든 렌더링의 시간을 측정해줌 → 어디서 느려지는지 확인 가능

### Redux Developer Tools

Redux store에 있던 state를 전부 확인 가능

dispatch 할때 뭐가 어떻게 바뀌었는지 로그를 작성 → store이 복잡해지면 유용

### lazy import

리액트 코드를 다 짜면 npm run build 입력해서 html, js 파일로 변환 해야됨

그러나 리액트 특성 상, html, js c파일이 하나만 생성되므로 그 안에 App/ Detail… 이런 파일이 좀 크다. 따라서 로딩 속도가 느려질 수 있음 

이때, js파일을 잘게 쪼개면 해결되는데, 메인 페이지에서 안 쓰이는 컴포넌트들은 lazy import로 해결할 수 있음

```jsx
import Detail from './routes/Detail.js'
import Cart from './routes/Cart.js'

// 위의 것을 이렇게 고치면 된다.
import {lazy, Suspense, useEffect, useState} from 'react'

const Detail = lazy( () => import('./routes/Detail.js') )
const Cart = lazy( () => import('./routes/Cart.js') )
```

여기서 lazy를 썼기 때문에 컴포넌트에서 지연시간이 발생할 수 있음. 이때는 대신 보여줄 html을 작성해 놓으면 된다.

1. Suspense import
2. Detail 컴포넌트 감싸고
3. fallback에는 로딩중일때 보여줄 html 작성

```jsx
<Suspense fallback={ <div>로딩중임</div> }>
  <Detail shoes={shoes} />
</Suspense>
```

---

### memo()로 컴포넌트 불필요한 재렌더링 막기

```jsx
import {memo, useState} from 'react'

let Child = memo( function(){
  console.log('재렌더링됨')
  return <div>자식임</div>
})

function Cart(){ 

  let [count, setCount] = useState(0)

  return (
    <Child />
    <button onClick={()=>{ setCount(count+1) }}> + </button>
  )
}
```

1. memo import
2. 원하는 컴포넌트 정의 부분을 memo로 감싸기

→ Child로 전송되는 props가 변하는 경우에만 재렌더링됨

하지만, props가 복잡한 경우에는 적합하지 않을 수 있음

### useMemo()

useEffect와 비슷 → 컴포넌트 로드시 1회만 실행하고 싶은 코드가 있으면 실행

```jsx
import {useMemo, useState} from 'react'

function 함수(){
  return 반복문10억번돌린결과
}

function Cart(){ 

  let result = useMemo(()=>{ return 함수() }, [])

  return (
    <Child />
    <button onClick={()=>{ setCount(count+1) }}> + </button>
  )
}
```

---

### 일관된 batching

state 변경 함수를 연달아서 사용하면 재렌더링이 매번 되어야 하지만, 재렌더링이 방지되고 1회만 실행 → batching

하지만, ajax요청과 setTimeout안에 state변경함수가 있는 경우 batching이 일어나지 않는다.

---

### useTransition

```jsx
import {useState} from 'react'

let a = new Array(10000).fill(0)

function App(){
  let [name, setName] = useState('')
  
  return (
    <div>
      <input onChange={ (e)=>{ setName(e.target.value) }}/>
      {
        a.map(()=>{
          return <div>{name}</div>
        })
      }
    </div>
  )
}
```

input 하면 그 글자를 div안에 만 개 집어 넣어줘야 하는데 렌더링이 오래 걸릴 것임.

```jsx
import {useState, useTransition} from 'react'

let a = new Array(10000).fill(0)

function App(){
  let [name, setName] = useState('')
  let [isPending, startTransition] = useTransition()
  
  return (
    <div>
      <input onChange={ (e)=>{ 
      // 이 부분을 약간 늦게 시작해줌
        startTransition(()=>{
          setName(e.target.value) 
        })
      }}/>

      {
	      isPending ? "로딩중" :
        a.map(()=>{
          return <div>{name}</div>
        })
      }
    </div>
  )
}
```

1. input을 먼저 보여주고
2. div를 만 개 만들어준다. (startTransition을 나중에 실행해줌)

isPending은 startTransition이 처리중일 때 true로 변함. true면 로딩중을 보여주고 다 처리하면 함수를 처리해줌  → 좀 더 매끄러울 듯.

---

### useDeferredValue

```jsx
import {useState, useTransition, useDeferredValue} from 'react'

let a = new Array(10000).fill(0)

function App(){
  let [name, setName] = useState('')
  let state1 = useDeferredValue(name)
  
  return (
    <div>
      <input onChange={ (e)=>{ 
          setName(e.target.value) 
      }}/>

      {
        a.map(()=>{
          return <div>{state1}</div>
        })
      }
    </div>
  )
}
```

useDeferredValue 안에 state를 집어 넣으면 그 state가 변동 사항이 생겼을 때 나중에 처리해줌