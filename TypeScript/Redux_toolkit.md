# React + Type Script : Redux toolkit

### (구)state, reducer 의 타입 지정

```tsx
// index.ts
import React from 'react';
import ReactDOM from 'react-dom';
import { Provider } from 'react-redux';
import { createStore } from 'redux';

interface Counter {
  count: number;
}

const 초기값: Counter = { count: 0 };

function reducer(state = 초기값, action: any) {
  if (action.type === '증가') {
    return { count: state.count + 1 };
  } else if (action.type === '감소') {
    return { count: state.count - 1 };
  } else {
    return state; // 초기값을 유지
  }
}

const store = createStore(reducer);

export type RootState = ReturnType<typeof store.getState>;

import App from './App'; // App 컴포넌트 import

ReactDOM.render(
  <React.StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </React.StrictMode>,
  document.getElementById('root')
);
```

1. `초기값` 오른쪽에 타입 지정 필수
2. reducer함수는 `state`, `action` 이 두개의 파라미터를 잘 지정해 주기.
3. reducer함수의 return 타입도 지정

### state 꺼낼 때

redux에 있는 `state`를 가져오려면 `useSelector`을 사용해주기

`state`를 변경하려면 `useDispatch` 훅을 쓰면 `dispatch`를 간단히 날릴 수 있다.

```tsx
// App.tsx

import React from 'react';
import { useDispatch, useSelector } from 'react-redux';
import { RootState } from './index';

function App() {
  const count = useSelector((state: RootState) => state.count); 
  const dispatch = useDispatch();

  return (
    <div className="App">
      {count}
      <button onClick={() => dispatch({ type: '증가' })}>버튼</button>
    </div>
  );
}

export default App;
```

1. `useSelector()` 안에 파라미터에 하기
    
    `state`는 `index.ts`에서 타입을 `export`해와도 됨. 
    
    `export type RootState = ReturnType<typeof store.getState>;` 
    
    `store`의 타입을 미리 지정한 것.
    
2. `useDispatch`타입 지정해도 되고 지정 안해도 됨.

### (신)**state, reducer 만들 때 타입 지정**

```tsx
npm install @reduxjs/toolkit 
```

```tsx
// index.ts
import React from 'react';
import ReactDOM from 'react-dom/client';
import { createSlice, configureStore, PayloadAction } from '@reduxjs/toolkit';
import { Provider } from 'react-redux';
import App from './App'

interface CounterState {
  count: number;
  user: string;
}
const 초기값 : CounterState = { count: 0, user: 'kim' };

const counterSlice = createSlice({
  name: 'counter',
  initialState: 초기값,
  reducers: {
    increment(state) {
      state.count += 1;
    },
    decrement(state) {
      state.count -= 1;
    },
    incrementByAmount(state, action: PayloadAction<number>) {
      state.count += action.payload;
    }
  }
});

let store = configureStore({
  reducer: {
    counter: counterSlice.reducer
  }
});

// state 타입을 export (컴포넌트에서 useSelector 사용 시 필요)
export type RootState = ReturnType<typeof store.getState>;
export type AppDispatch = typeof store.dispatch; // 

// 액션 생성자 export
export const { increment, decrement, incrementByAmount } = counterSlice.actions;
export default store;

// 7️⃣ ReactDOM 설정
const container = document.getElementById('root') as HTMLElement;
const root = ReactDOM.createRoot(container);

root.render(
  <React.StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </React.StrictMode> 
);
```

1. `createSlice(`) 로 slice 만들기. slice는 `state`와 `reducer`를 합쳐 놓은 것
2. slice 안에는 `slice 이름`, `state초기값`, `reducer`가 정확한 이름으로 들어가야 함.맘대로 바꾸기는 안돼
3. `state`는 일반 형태. `reducer`는 함수 형태로 만들기. **첫 파라미터는 state, 둘째는 actions**가 자동으로 부여 됨.
4. 다 만든 것들은 `configureStore` 안에 등록
5. 내가 만들어둔 reducer를 쓰고 싶으면 reducer 안의 함수 명을 export 해주시면 됩니다.

- 타입 지정
1. state 초기값 타입 지정
2. action 파라미터의 타입 지정 `PayloadAction<>` 

### state 꺼낼 때

```tsx
// App.tsx

import { useDispatch, useSelector } from 'react-redux'
import {RootState, increment} from './index'

function App() {

  const 꺼내온거 = useSelector( (state :RootState) => state.counter.count);
	const dispatch = useDispatch<AppDispatch>();

  return (
    <div className="App">
      {꺼내온거}
      <button onClick={()=>{dispatch(increment())}}>버튼</button>
    </div>
  );
} 

export default App;
```

- 타입 지정
1. `useSelector()` 안의 파라미터에 타입 지정
    
    (위와 방식 똑같)
    
2. `useDispatch()`
`const dispatch = useDispatch<AppDispatch>();`