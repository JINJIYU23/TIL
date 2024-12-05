# 탭 UI를 이용한 if문 배우기

사실 나는 state를 변경하는 걸 조금 어려워하는 것 같다.ㅠㅠ

일단 동적인 UI를 만드는 것은

1. **html css로 디자인 미리 완성해놓고**
2. **UI의 현재 상태를 저장할 state 하나 만들고**
3. **state에 따라서 UI가 어떻게 보일지 작성**

tab 디자인 (bootstrap)

```jsx
{/* 탭 */}
<Nav variant="tabs"  defaultActiveKey="link0">
  <Nav.Item>
   <Nav.Link eventKey="link0" onClick={() => {setTab(0)}}>버튼0</Nav.Link>
  </Nav.Item>
  <Nav.Item>
   <Nav.Link eventKey="link1" onClick={() => {setTab(1)}}>버튼1</Nav.Link>
  </Nav.Item>
  <Nav.Item>
    <Nav.Link eventKey="link2" onClick={() => {setTab(2)}}>버튼2</Nav.Link>
  </Nav.Item>
 </Nav>
```

UI의 현재 상태를 저장할 state 만들기

```jsx
// 탭
let[tab, setTab] = useState(0);
```

내용 0이 보이거나, 내용 1, 내용 2가 보일 수 있도록 변경

```jsx

// 외부에 if문 쓸 수 있는데 안에서 쓴 tab은 props로 불러와줘야 함
function TabContent(props) {
  if (props.tab == 0) {
    return <div>내용0</div>
  } else if (props.tab == 1) {
    return <div>내용1</div>
  }else if (props.tab == 2) {
    return <div>내용2</div>
  }  
}
```

이제 state를 갖다 쓰면 

```jsx
<TabContent tab = {tab}></TabContent>
```

근데 이게 어려운 것 같다. 지금  현재 tab이 detail안에 있기 때문에

이걸 다시 TabContent에 넣어줘야 한다. 따라서 tab ={tab}을 써줌.

if문 없이 바꿔주는 방법은

```jsx
function TabContent(props){
  return [ <div>내용0</div>, <div>내용1</div>, <div>내용2</div> ][props.탭]
}
```

탭이 0, 1, 2 로 바뀔 때마다 내용0, 내용1, 내용2를 보여줄 수 있기 때문.