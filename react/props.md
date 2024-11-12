# props

### 지금 누른 글 제목이 모달창 안에 뜨게 코드 짜기

1. html, css로 미리 디자인
2. 현재 UI상태를 state로 만들어 놓기

```jsx
let[title, setTitle] = useState(0);
```

1. state에 따라서 UI가 어떻게 보일지 작성

```jsx
function App (){
  return (
    <div>
      { 
        글제목.map(function(a, i){
          return (
          <div className="list">
            <h4 onClick={()=>{ setModal(true); setTitle(i); }}>{ 글제목[i] }</h4>
            <p>2월 18일 발행</p>
          </div> )
        }) 
      }
    </div>
  )
}
```

- props쓸 때 주의 점

html을 불러올 때 사용했던 <Modal/>여기에 state들을 불러와서 미리 적어줘야 함

```jsx
<Modal color={'skyblue'} 글제목 = {글제목} 글제목변경 = {글제목변경} title = {title}/>
```

Modal을 정의해 준 function에서 파라미터처럼 props 불러와서

가져와서 쓰고 싶은 state에는 꼭 props.state명 이렇게 써줘야 함

```jsx
function Modal(props) {
  return(
    <div className="modal" style={{background : props.color}}>
      <h4>{props.글제목[props.title]}</h4>
      <p>날짜</p>
      <p>상세 내용</p>
      <button onClick={() => { 
        // 제목 수정을 누르면 여자 코트 추천으로 바뀌는 방식
          let copy1 = [...props.글제목];
          copy1[0] = '여자 코트 추천';
          props.글제목변경(copy1); }
      }>제목 수정</button>
    </div>
  )
```