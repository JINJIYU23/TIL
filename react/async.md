# state 변경 함수 사용시 주의점 : async

자바스크립트는 코드를 작성한 순서대로 실행이 되는 특징을 가지고 있지만 ajax, 이벤트리스너, setTimeout 등 함수를 사용하면 비동기적으로 작동한다.(순서대로 작동하지 않음. 시간이 오래 걸리는 함수들이어서)

리액트의 setState 함수는 전부 **비동기적**으로 처리 된다.

버튼을 누를 때마다

(1) count라는 state를 +1  (버튼누른 횟수 기록용)

(2) age라는 state도 +1

(3) 근데 count 가 3 이상이면 더 이상 age라는 state를 1 더하지 말도록

```jsx
<button onClick={()=>{

  setCount(count+1);
  if ( count < 3 ) {
    setAge(age+1);
  }
         
}}>누르면한살먹기</button>
```

이런식으로 코드를 짜게 된다면, count가 3일 때도 age + 1을 해주는 현상을 보인다. 

→ state 변경함수는 비동기적이기 때문이다. 

이때의 해결책은 useEffect를 사용해주는 것이다.

```jsx
<button onClick={()=>{

  setCount(count+1);

}}>누르면한살먹기</button> 

useEffect(()=>{
  if ( count != 0 && count < 3 ) {
    setAge(age+1)
  }
 }, [count]) 
```

문제는 useEffect 저렇게 써도 처음 페이지 로드될 때도 한번 실행이 되기 때문에 의도치 않은 버그가 발생할 수 있음, 그래서 처음 페이지 로드시 useEffect 실행을 막는 코드를 알아서 검색해서 적용하셔도 되고 아니면 count라는 state를 또 활용하셔도 됩니다.

→ count가 0일 때는 (페이지 처음 로드 되었을때는) 내부 코드를 동작 X