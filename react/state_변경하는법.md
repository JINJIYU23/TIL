# State 변경하는 법

일단, Java script처럼 onclick기능을 추가 할 수 있다.

`<div onClick={실행할함수}>`

1. onClick임
2. {}를 사용하여 안에 함수를 넣어줘야 작동함
    
    → 함수는 다른 곳에서 함수를 만들어서 집어넣어줘도 됨
    

```jsx
<div onClick={ function(){ 실행할코드 } }>
<div onClick={ () => { 실행할코드 } }>
```

함수를 외부에 따로 안 만들고 위에처럼 쓸 수 있움.

state변경할 때는 state변경 함수를 써서 변경해야 함.

`let [ 따봉, 따봉변경 ] = useState(0);` 

여기서 ‘따봉변경’을 변경해줘야함

```jsx
function App(){

let [ 따봉, 따봉변경 ] = useState(0);
return (
<h4> { 글제목[0] } <span onClick={ ()=>{ 따봉변경(따봉 + 1) } } >👍</span> { 따봉 }</h4>
)
}
```