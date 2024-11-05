# array, object변경하는 법

```jsx
function App(){
  
  let [글제목, 글제목변경] = useState( ['남자코트 추천', '강남 우동맛집', '파이썬 독학'] );  
  
  return (
    <button onClick={ ()=>{ 
      let copy = [...글제목];
      copy[0] = '여자코트 추천';
      글제목변경(copy)
    } }> 수정버튼 </button>
  )
}
```

복사본 만들고 […]이게 중요함  → **spread operator**

1. array, object 자료형 왼쪽에 붙일 수 있음
2. array, object 자료형을 복사할 때 많이 사용
3. 완전히 독립적인 복사본 생성 가능

그래서 그냥 복사해서 쓰고 싶으면 저렇게 써주도록 하자.

- 가나다순 정렬

```jsx
      <button onClick={() => {
        let copy0 = [...글제목];
        글제목변경(copy0 = copy0.sort());
      }}>가나다순 정렬</button>
```