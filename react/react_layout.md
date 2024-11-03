# React 레이아웃

JSX는 html 대신 사용하는 html같은 언어

- html에 class를 넣을 땐 className

```jsx
      <div className = "black-nav">
        <h4 style = {{ color:'red', fontSize : '16px' }}>블로그</h4>
      </div>
```

- 변수를 html 안에 넣고 싶으면 { } → 데이터 바인딩
    
    여기저기 사용할 수 있음
    

```
let post = '강남 우동 맛집';
  

  return (
    <div className="App">
      <div className = "black-nav">
        <h4 style = {{ color:'red', fontSize : '16px' }}>블로그</h4>
      </div>
      <h4>{ post }</h4>
    </div>
  );
}
```

- html 에 css속성을 넣고 싶으면 style = {{ }}
    
    { 속성명 : '속성값' }
    
    font-size 처럼 대쉬 기호를 쓸 수 없기 때문에 fontSize 이런식으로 써야함
    

```jsx
<h4 style = {{ color:'red', fontSize : '16px' }}>블로그</h4>
```