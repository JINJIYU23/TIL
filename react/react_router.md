# react router : navigate, nested routes, outlet

1. 페이지 간 이동기능 : useNavigate()

```jsx
let navigate = useNavigate();

(생략)
 <Nav.Link onClick={() => { navigate('/')}}>Home</Nav.Link>
 <Nav.Link onClick={() => { navigate('/detail')}}>Detail</Nav.Link>
```

눌렀을 때 이동할 수 있도록 해준다.

1. 없는 페이지를 띄워줄 땐  :  path = ‘*’

```jsx
<Route path='*' element = {<div>없는 페이지입니다.</div>}></Route>
```

1. 서브 경로를 말들 때 : nested routes

```jsx
<Route path="/about" element={ <About/> } >  
  <Route path="member" element={ <div>멤버들</div> } />
  <Route path="location" element={ <div>회사위치</div> } />
</Route>
```

route안에 route를 집어 넣어서 서브 경로로 이동할 수 있음

→ 이때는 꼭 Outlet과 함께 써야 하는데

<About/>함수를 만든 곳에 

```jsx
function About(){
  return (
    <div>
      <h4>about페이지임</h4>
      <Outlet></Outlet>
    </div>
  )
}
```

이런식으로 작성한 후 nested route에 의해 하위 페이지로 이동할 수 있다.