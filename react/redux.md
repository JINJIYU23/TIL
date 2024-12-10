# Redux를 이용한 장바구니 페이지 만들기

장바구니 페이지 만들기 

페이지가 하나 필요할 땐 <Routes>

```jsx
<Route path="/cart" element={ <Cart/> } /> 
```

입력해주면 장바구니 페이지 생성 완료

Cart.js에 컴포넌트 만들어서 넣어줄 것임

---

일단, Redux는 props 없이 state를 공유할 수 있게 도와주는 라이브러리

### Redux 설치

```jsx
npm install @reduxjs/toolkit@1.8.1 react-redux 
```

터미널에 입력, 단 package.json파일에서 react와 react-dom이 18.1.X이상이면 사용 가능

아무 파일(store.js)에

```jsx
import { configureStore } from '@reduxjs/toolkit'

export default configureStore({
  reducer: { }
}) 
```

이거 만들어주고 사용 가능.

다음 index.js파일에 가서 

```jsx
import { Provider } from "react-redux";
import store from './store.js'

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <Provider store={store}>
      <BrowserRouter>
        <App />
      </BrowserRouter>
    </Provider>
  </React.StrictMode>
); 
```

Provider라는 컴포넌트와 store.js파일을 import

다음으로는 <Provider>로 <App>을 감싸주면 됨.

---

### Redux store에 state 보관하는 법

1. createSlice()로 state 만들기
2. configureStore() 안에 등록

```jsx
import { configureStore, createSlice } from '@reduxjs/toolkit'

// { name : 'state이름', initialState : 'state값' }
let user = createSlice({
  name : 'user',
  initialState : 'kim'
})

//{ 작명 : createSlice만든거.reducer }
export default configureStore({
  reducer: {
    user : user.reducer
  }
})
```

---

### Redux store에 있던 state 가져다 쓰는 법

Cart.js에서 

```jsx
import { useSelector } from "react-redux"

function Cart(){
  let a = useSelector((state) => { return state } )
  // let a = useSelector((state) => state.user ) 이렇게 쓰면 더 편리함
  console.log(a)

  return (생략)
}
```

console.log로 찍어보면 {user : kim} 출력됨

데이터 바인딩까지 해보면

```jsx
[
  {id : 0, name : 'White and Black', count : 2},
  {id : 2, name : 'Grey Yordan', count : 1}
]    // 이걸 데이터 바인딩 해 볼 것임.
```

일단 store.js파일에 state를 넣어줘야 함

```jsx
let info  = createSlice({
    name : 'info',
    initialState :
    [
        {id : 0, name : 'White and Black', count : 2},
        {id : 2, name : 'Grey Yordan', count : 1}
    ] 
})

export default configureStore({
  reducer: {
   user : user.reducer,
   stock : stock.reducer,
   info : info.reducer
   }
}) 
```

처음에는 헷갈려서 데이터를 initialState에 넣지 않고 다른 방식으로 넣었으나 아무리 긴 데이터도 그냥 저기에 넣으면 된다는 것을 알게 되었다.

이름을 info로 정해주고 export까지 해주면 내보내기까지 완료

```jsx
import { Table } from  'react-bootstrap';
import { useDispatch, useSelector } from 'react-redux';

function Cart() {

// 데이터 바인딩
    let data = useSelector((state) => { return state })

    return(
        <div>
            <Table>
                <thead>
                    <tr>
                    <th>#</th>
                    <th>상품명</th>
                    <th>수량</th>
                    <th>변경하기</th>
                    </tr>
                </thead>
                <tbody>
                    {
                        data.info.map(function(a, i){
                            return (
                                <tr>
                                <td>{data.info[i].id + 1}</td>
                                <td>{data.info[i].name}</td>
                                <td>{data.info[i].count}</td>
                                <td>
                                </td>
                                </tr>
                            )
                    })}
                </tbody>
            </Table> 
        </div>
    )
}

export default Cart;
```

데이터를 useSelector로 받아온다. ( data 안에는 store.js에 있는 모든 데이터들이 다 담겨있음)

거기에서 필요한 data.info를 데이터 바인딩 해주면 된다. 

map함수를 이용하면 데이터의 수 만큼 반복문을 이용해서 표를 생성해줄 수 있기 때문에 써주고 data.info[i]를 한다면 각 순번대로 데이터 바인딩 가능.

data.info[i].id,, 이런거 해주면 그 안에 아이디 값, 이름 , 개수 등을 불러올 수 있음

뭔가 이걸 내가 했다니 조금 뿌듯하다.

생각해보면 기초에 배운게 진짜 계속 쓰이는 것 같다.

---

### Redux store에 state 변경하는 법 (조금 까다로움)

1. store.js(데이터가 들어있는 파일)안에 state를 수정하는 함수 만들어주기
    
    reducers :{ } ← 여기에 변할 것 적어주기. 
    

```jsx
let user = createSlice({
  name : 'user',
  initialState : 'kim',
  reducers : {
    changeName(state){
      return 'john ' + state
    }
  }
})

// 바뀐 이름을 불러오는 것(state 변경)
// slice이름.actions라고 적으면 됨
export let { changeName } = user.actions 
```

1. export 바로 해주기 (변수를 이용해서 보내기)
2. import해서 사용, dispatch()로 감싸기
    
    Cart.js에서
    
    store.js에서 원하는 state 변경 함수 가져오기(여기서는 changeName)
    
    useDispatch 라이브러리가져오기
    
    dispatch(state변경함수()) 해주면 변경완료 (여기서는  changeName)
    

```jsx
import { useDispatch, useSelector } from "react-redux"
import { changeName } from "./../store.js"

(생략) 

let dispatch = useDispatch()
<button onClick={()=>{
// state 변경하는 dispatch
  dispatch(changeName())
}}>+</button> 
```

---

### state가 object/array일 때 변경하는 법

```jsx
let user = createSlice({
  name : 'user',
  initialState : {name : 'kim', age : 20},
  reducers : {
    changeName(state){
      return {name : 'park', age : 20}
    }
  }
})
```

이렇게 변경해도 잘 되지만,

```jsx
let user = createSlice({
  name : 'user',
  initialState : {name : 'kim', age : 20},
  reducers : {
    changeName(state){
      state.name = 'park'
    }
  }
})
```

state를 직접 수정해도 변경 가능.

그냥 state를 변경하는 것보다  object/ array를 변경하는 것이 더 간편한 것 같다.

- 버튼을 누르면 age 항목이 +1 되도록 만들기

```jsx
let user = createSlice({
  name : 'user',
  initialState : {name : 'kim', age : 20},
  reducers : {
    increase(state){
      state.age += 1
    }
  }
}) 
```

이렇게 해주고 increase를 export한 후 필요한 곳에 import해준 뒤, dispatch(increase())하면 바로 +1 가능

state 변경 함수가 여러 개 필요하면,

**파라미터 문법** 사용 가능

```jsx
let user = createSlice({
  name : 'user',
  initialState : {name : 'kim', age : 20},
  reducers : {
    increase(state, action){
      state.age += action.payload
    }
  }
})
```

여기에 이제 increase()함수를 써줄 때,

increase(10), increase(200) 이런 식으로 써주면 각각 + 10, + 200 이렇게 쓸 수 있다.

근데 꼭 .payload 를 붙여줄 것.

---

### 수량 + 1 만들기

Cart.js에 

```jsx
<button onClick={()=>{
 dispatch(changeCount(data.info[i].id))
}}>+</button>
```

data.info[i].id : 누른 상품의 id를 전송하는 것 (payload 임)

userSlice.js에서

```jsx
    reducers : {
        changeCount(state, action) {
            let number = state.findIndex((x) => { return x.id == action.payload})
            state[number].count++
        }
```

payload와 같은 id를 state에서 찾아서 그 index를 numder로 저장하고 그 state의 수량을 1씩 더해준다.(약간은 복잡하고 어려움)

findIndex()는 array 뒤에 붙일 수 있는데

- 안에 콜백함수넣고 return 뒤에 조건식도 넣기
- x라는 파라미터는 array 안에 있던 하나하나의 자료
- array에 있던 자료를 다 꺼내서 조건식에 대입해보는데 조건식이 참이면 그게 몇 번째 자료인지 알려줌

→ 그래서 위의 코드는 x.id와 payload가 같으면 그게 몇 번째 자료인지 변수에 저장

### 주문 버튼 누르면 state에 새로운 상품 추가

detail에서 장바구니 추가 버튼을 누르면 cart에 상품이 추가 되도록

```jsx
import { createSlice } from '@reduxjs/toolkit'

let info  = createSlice({
    name : 'info',
    initialState :
    [
        {id : 0, name : 'White and Black', count : 2},
        {id : 2, name : 'Grey Yordan', count : 1}
    ],
    reducers : {
        changeCount(state, action) {
            // 조금은 문제가 생길 수 있는 코드
            //state[action.payload].count++

            let number = state.findIndex((x) => { return x.id == action.payload})
            state[number].count++
        },
        addProduct(state, action) {
            state.push(action.payload)
        }
    }

})

export let { changeCount, addProduct } = info.actions;
export default info;
```

state.push()해주기

action.payload에는 (→ {id : 1, name : 'Red Knit', count : 1})

```jsx
<button className="btn btn-danger" 
                onClick={() => {dispatch(addProduct(
                  {id : 1, name : 'Red Knit', count : 1}
))}}>주문하기</button> 
```

addProduct함수를 추가해주면 됨.

근데, 이때 cart 페이지를 url로 이동하면 안됨. 버튼을 하나 만들어서 페이지를 이동 할 경우에만 보인다. 왜냐면 새로 고침 되면 state 도 초기값으로 변경된다.