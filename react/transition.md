# transition : 애니메이션

애니메이션(효과)를 만들고 싶으면 

1. 애니메이션 동작 전 스타일 className에 넣어놓기
2. 애니메이션 동작 후 스타일 className에 넣어놓기
3. transition 속성 추가 (아마도 동작 후 스타일에 추가)
4. 원할 때 탈부착 기능 추가하기

- tab을 누르면 내용의 투명도가 0에서 1로 바뀌는 애니메이션 적용하기

여기서 4번이 까다롭다고 생각이 듬.

```
// 1,2,3까지 끝
.start {
  opacity: 0;
}

.end {
  opacity: 1;
  transition:  opacity 1s;
}
```

원할 때 end를 넣어주면 된다. 근데 그 과정이 꽤나 어려운 것 같다.

→ useEffect를 써주면 특정 state 또는 props가 변할 때마다 코드 실행이 가능하다

```jsx
function TabContent(props) {

  let[fade, setFade] = useState('')

  useEffect(() => {
    setTimeout(() => {setFade('end')}, 100)

    return () => {
      setFade('')
    }
  }, [props.tab])

   return ( <div className={'start ' + fade}>
    {[<div>{props.shoes[0].title}</div>, <div>내용 1</div>, <div>내용2</div>][props.tab]}
   </div>)
}
```

일단 fade를 공백으로 바꾸고 0.1초 시간이 지나면 다시 end를 부착해서 효과를 적용할 수 있음…