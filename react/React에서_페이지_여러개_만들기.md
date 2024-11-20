# react에서 페이지 여러 개 만들기

리액트는 html 파일을 하나만 사용

이때 **react-router-dom**이라는 라이브러리를 설치해서 구현

설치한 후, index.js라는 파일에 가서 

<BrowerRouter>로 <App/>을 감싸주기.

```jsx
import { BrowserRouter } from 'react-router-dom';
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <BrowserRouter>
    <App />
    </BrowserRouter>
  </React.StrictMode>
);

```

```jsx
import { Routes, Route, Link } from 'react-router-dom';

function App(){
  return (
    (생략)
    <Routes>
	    <Route path="/" element={ <div>메인페이지에서 보여줄거</div> } /> 
      <Route path="/detail" element={ <div>상세페이지</div> } />
      <Route path="/about" element={ <div>어바웃페이지</div> } />
    </Routes>
  )
}
```

이건 메인, 상세 페이지, 어바웃 페이지. 총 3개의 페이지를 새로 만든 것.

메인 페이지는 맨 위

페이지 이동 버튼은 Link

```jsx
<Link to="/">홈</Link>
<Link to="/detail">상세페이지</Link>
```