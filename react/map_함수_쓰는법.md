# map()함수 쓰는 법

- 모든 array자료형 오른쪽에 map()을 붙일 수 있음

```jsx
   // map : array자료 개수만큼 함수안의 코드 실행
   [1,2,3].map(function(){
     console.log(1);
   });
```

→ console.log(1) 3번 출력

- 함수의 파라미터는 array안의 자료

```jsx
   [1,2,3].map(function(a){
     console.log(a);
   });
```

→ 1,2,3이 출력 됨

- return안에 뭐를 적으면 array로 담아줌

```
   console.log(
   [1,2,3].map(function(a){
    return '123123';
  }));
```

→ length가 3이라 3번 담아줌

![image.png](image.png)

- map()은 반복문의 기능도 할 수 있어서 반복되는 html자료를 축약하여 나타낼 수 있다.

```jsx
      {/* html을 map으로 여러개 만드는 법 (반복문) */}

      {
        글제목.map(function(a, i){
          return(
            <div className="list" key={i}>
              <h4 onClick={() => {
                setModal(true) 
                // 한번 더 클릭했을 때 모달창 닫기
                modal === true ? setModal(false) : setModal(true) ;
              }}> { 글제목[i] } <span onClick={ () => {
                // 따봉이 array자료일 경우에는 복사본을 만들어서 해야함
                let copy = [...따봉];
                copy[i] = copy[i] + 1;
                따봉변경(copy)}}>👍 { 따봉[i] }</span></h4>
              <p>2월 17일 발행</p>
            </div>
          )
        })
      }
```

map(function(a,i){}는 파라미터를 a, i 두 개를 쓸 수 있음

a 는 array에 있는 자료들을 나타내고

i 는 정수 (length만큼일 듯)

*** 주의 점으로는 map을 반복 생성한 html에서는 

```jsx
<div className="list" key={i}> 
```

를 꼭 써줘야함!
→ 리액트가 <div>들을 구분 가능