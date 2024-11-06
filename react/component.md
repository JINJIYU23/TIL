# Component : 많은 div를 한 단어로 줄이기

```jsx
return(
  <div></div>
  <div></div>
)
```

이거는 안됨, return안에 div를 두 개 나란히 쓸 수 없음

```jsx
return(
  <div>
    <div></div>
    <div></div>
  </div>
)
```

div를 두 개 적고 싶다면 앞에 div로 감싸준 뒤 사용 가능

또는  <> </> 이걸로 감싸도 됨 → fragment 문법

- 복잡한 html을 한 단어로 축약해주는 component문법

```jsx
function App (){
  return (
    <div>
      <Modal></Modal>  // 축약한 html 함수
    </div>
  )
}

function Modal(){
  return (
    <div className="modal">
      <h4>제목</h4>
      <p>날짜</p>
      <p>상세내용</p>
    </div>
  )
}
```

외부에 function만들고 이름 붙여준 뒤 빼고 싶은 html을 써서 쓰고 싶은 곳에 써주면 됨

## ⚠️ component만들 때 주의점

1. 작명 할 땐 보통 대문자로 
2. return안에 html 태그들 여러 개 사용 불가능 
3. function App() {} 내부에 만들면 안됨

## 👍 component 어디에 쓰면 좋을까?

1. 반복되는 html
2. 내용이 자주 변경될 것 같은 html
3. 다른 페이지를 만들 때 그 페이지의 html내용을 하나의 component 로
4. 다른 팀원과 협업 할 때

## ⛔ component의 단점

state를 쓰고 싶어서 외부 함수에 써주면 안됨.

한 function안에 있던 내용을 다른 function에서 사용하면 오류 발생

→ props문법으로 해결 가능 (아직 안배움 !!!)