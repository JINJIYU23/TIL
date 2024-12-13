# localStorage

새로고침 하면 모든 state 데이터는 리셋됨

→ DB에 저장하거나 유저의 브라우저에 몰래 정보를 저장하는 localstorage를 사용

개발자 도구에서 Application탭에 들어가면 가능

object 자료랑 비슷하게 key/value의 형태로 저장

```jsx
// 추가
localStorage.setItem('데이터이름', '데이터');
// 읽기
localStorage.getItem('데이터이름');
// 삭제
localStorage.removeItem('데이터이름')
```

문자만 저장할 수 있기 때문에 array/object자료를 저장하려면 **JSON자료**로 저장하면 됨

```jsx
// localStorage로 자료 저장
let obj = {name : 'kim'}
localStorage.setItem('data', JSON.stringify(obj))
let 꺼낸거 = localStorage.getItem('data')

// JOSN -> array/object변환
console.log(JSON.parse(꺼낸거));
```

데이터를 JSON.stringify()에 집어 넣으면 됨.

→ 결과 : {”name” : “kim”}

꺼낼 때는 array/object로 변환시켜서 꺼내야 됨

JSON.parse(꺼낸거) 이렇게 쓰면 됨

- 최근 본 상품 UI 기능 만들기

상세페이지 들어가면 현재 페이지에 있는 상품 id를 localStorage에 저장

저장할 땐 array 자료형

만약에 0번 1번 상품을 보았다면 [0,1] 이런 데이터가 localStorage에 저장

일단, App.js에 

```jsx
  // 방문사이트 접속기록
  useEffect(() => {
    localStorage.setItem('watched',JSON.stringify([]))
  },[])
```

비어 있는 array를 만들어 놓고, array 자료형으로 집어 넣기 위해 비어있는 [] 를 만들어주기.

다음, Detail.js에 가서

1. useEffect는 react가 렌더링 될 때마다 특정 작업을 처리할 수 있게 해줌, 저장한 데이터를 읽기 (getItem)
2. 데이터를 문자로 변환시키 위해 JSON.parse()
3. 해당 아이디를 넣어주기 (옛날에 useParam을 이용해서 URL로 찾았던 id를 저장했던 idid의 id를 넣어주면 됨…)
4. 그 담에 이게 같은 페이지를 여러 번 누르면 중복으로 ([0,1,1,1,1]) 저장될 수 있기 때문에 중복 제거하고 그걸 다시 array 형태로 저장해서 localStorage에 넣어주기 

```jsx
    // 최근 본 상품 찾기
    useEffect(() => {
        // getItem은 읽기
        let 꺼낸거 = localStorage.getItem('watched');
        // JSON 자료를 array/object자료로 변환 
        꺼낸거 = JSON.parse(꺼낸거)
        // 해당 id를 넣어줌 (detail/1...등)
        꺼낸거.push(idid.id)
        let set = Array.from(new Set(꺼낸거))
        localStorage.setItem('watched', JSON.stringify(set))
    },[])
```