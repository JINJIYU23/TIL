# ajax

**서버** : 유저가 데이터를 요청하면 데이터를 보여주는 프로그램

데이터를 가져올 때 : GET

데이터를 서버로 보낼 때 : POST

어떤 데이터를 볼지 : URL

**ajax :** 서버에 GET, POST요청을 할 때 새로 고침 없이 데이터를 주고 받을 수 있는 간단한 브라우저 기능

- AJAX로 GET/POST요청할 때 **axios** 외부 라이브러리 쓰기

```jsx
npm install axios // 터미널에 입력하면 설치 완료

import axios from 'axios'

function App(){
  return (
    <button onClick={()=>{
      axios.get('https://codingapple1.github.io/shop/data2.json').then((결과)=>{
        console.log(결과.data)
      })
      .catch(()=>{
        console.log('실패함')
      })
    }}>버튼</button>
  )
}
```

json파일에 있는 데이터를 가져온 것임.

1. axios를 쓰려면 상단에 import해주고
2. axios.get('URL')해주면 그 URL로 GET  요청이 됨.
3. 데이터를 가져 온 것은 결과.data에 있음
4. 실패했을 경우 실행하는 코드는 .catch()에 적으면 된다.

---

### 서버에서 데이터 가져와서 상품 html 3개 더 생성하기

```jsx
let [shoes, setShoes] = useState(data);

<button onClick={() => {
              axios.get('https://codingapple1.github.io/shop/data2.json')
              .then((result) => {
                let copy = [...shoes, ...result.data];
                setShoes(copy);
              })
              // 데이터를 가져오기 살패했을 경우,
              .catch(() => {
                console.log('실패함')
              })

              // 동시에 ajax 요청 여러개 하려면
              //Promise.all( [axios.get('URL1'), axios.get('URL2')] )

              // post 요청하는 법
              //axios.post('URL', {name : 'kim'})
            }}>버튼</button>
```

간략히 나타내면 이거다. 

일단, 

```jsx
 let copy = [...shoes, ...result.data];
```

이 부분이 굉장히 어려웠다.. 

일단 shoes의 사본을 만들고 그 안에 …를 이용해서 result.data를 뒤에 이어서 넣어준 것.

setShoes(copy);이건 이제 shoes의 state를 변경해 준 것.. (아직도 어렵다)

---

- post 요청하는 법

```jsx
axios.post('URL', {name : 'kim'})
```

이걸 실행하면 {name : ‘kim’}자료가 전송된다

완료했을 때 .then()을 뒤에 붙이면 뭐 할지 가능

- 동시에 ajax 요청 여러개 날리기

```jsx
Promise.all( [axios.get('URL1'), axios.get('URL2')] )
```