# react-query

```jsx
// 설치
npm install react-query@3

//import
import { QueryClient, QueryClientProvider, useQuery } from 'react-query'

(index.js)
import { QueryClient, QueryClientProvider } from "react-query"  //1번
const queryClient = new QueryClient()   //2번

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <QueryClientProvider client={queryClient}>  //3번
    <Provider store={store}>
      <BrowserRouter>
        <App />
      </BrowserRouter>
    </Provider>
  </QueryClientProvider>
); 

// 쓸때
 useQuery(['작명']), 
```

react-query로 ajax요청하기

```jsx
function App(){
  let result = useQuery('작명', ()=>
    axios.get('https://codingapple1.github.io/userdata.json')
    .then((a)=>{ return a.data })
  )
}

  return (
    <div>
      { result.isLoading && '로딩중' }
      { result.error && '에러남' }
      { result.data && result.data.name } // 성공
    </div>
  )
```

위에 useQuery 를 import 해 오고, useQuery로  ajax 요청 감싸주기

장점

1. ajax 요청 시 성공, 실패, 로딩 상태를 파악할 수 있음
2. 페이지 조정하고 여러 상황 때, 알아서 ajax 재요청을 해준다.(실시간데이터)
3. 실패 시, 재시도를 알아서 해줌
4. ajax로 가져온 결과는 state공유가 필요 없다